### Winforms get deployment version
    if (ApplicationDeployment.IsNetworkDeployed) 
    {
        var v = $"{ApplicationDeployment.CurrentDeployment.CurrentVersion}";
    }

### Create and write to temp file
    string myTempFile = Path.Combine(Path.GetTempPath(), "MyFile.txt");
    var cc = 10;
    while(cc>0)
    {
        using (StreamWriter sw = File.AppendText(myTempFile))
        {
            sw.WriteLine(cc--);
        }

    }
