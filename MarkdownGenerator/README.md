# MarkdownGenerator

```csharp
using System.Text;

// Console app to generate README.md files from Program.cs in each project directory
// and update the main README.md with links

string baseDirectory = Directory.GetCurrentDirectory();
string projectRoot = Directory.GetParent(baseDirectory)?.FullName ?? baseDirectory;

Console.WriteLine($"Scanning projects in: {projectRoot}");

var projectDirs = Directory.GetDirectories(projectRoot)
    .Where(dir => File.Exists(Path.Combine(dir, "Program.cs")))
    .ToList();

var generatedLinks = new List<string>();

foreach (var projectDir in projectDirs)
{
    string projectName = Path.GetFileName(projectDir);
    string programCsPath = Path.Combine(projectDir, "Program.cs");
    string readmePath = Path.Combine(projectDir, "README.md");

    Console.WriteLine($"Processing: {projectName}");

    // Read Program.cs content
    string code = File.ReadAllText(programCsPath);

    // Create README.md content
    var sb = new StringBuilder();
    sb.AppendLine($"# {projectName}");
    sb.AppendLine();
    sb.AppendLine("```csharp");
    sb.AppendLine(code);
    sb.AppendLine("```");

    // Write README.md
    File.WriteAllText(readmePath, sb.ToString());
    Console.WriteLine($"  ✓ Generated: {readmePath}");

    // Add to links list
    generatedLinks.Add($"- [{projectName}](./{projectName}/README.md)");
}

// Update main README.md
string mainReadmePath = Path.Combine(projectRoot, "README.md");
if (File.Exists(mainReadmePath))
{
    string mainReadme = File.ReadAllText(mainReadmePath);

    // Add section for project links if not exists
    string linksSection = "\n## Projects\n\n" + string.Join("\n", generatedLinks) + "\n";

    // Check if Projects section already exists
    if (mainReadme.Contains("## Projects"))
    {
        // Replace existing Projects section
        var lines = mainReadme.Split('\n').ToList();
        int startIndex = -1;
        int endIndex = -1;

        for (int i = 0; i < lines.Count; i++)
        {
            if (lines[i].Trim() == "## Projects")
            {
                startIndex = i;
            }
            else if (startIndex != -1 && lines[i].StartsWith("##") && i > startIndex)
            {
                endIndex = i;
                break;
            }
        }

        if (startIndex != -1)
        {
            if (endIndex == -1) endIndex = lines.Count;
            lines.RemoveRange(startIndex, endIndex - startIndex);
            lines.Insert(startIndex, linksSection.TrimEnd());
            mainReadme = string.Join("\n", lines);
        }
    }
    else
    {
        // Append to end
        mainReadme += linksSection;
    }

    File.WriteAllText(mainReadmePath, mainReadme);
    Console.WriteLine($"\n✓ Updated main README.md with project links");
}

Console.WriteLine($"\nDone! Generated {projectDirs.Count} README files.");

```
