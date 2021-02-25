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

### Dates
    // Originally from https://www.csharp-examples.net/string-format-datetime/
    // create date time 2008-03-09 16:05:07.123
    DateTime dt = new DateTime(2008, 3, 9, 16, 5, 7, 123);

    "{0:y yy yyy yyyy}", dt);  // "8 08 008 2008"   year
    "{0:M MM MMM MMMM}", dt);  // "3 03 Mar March"  month
    "{0:d dd ddd dddd}", dt);  // "9 09 Sun Sunday" day
    "{0:h hh H HH}",     dt);  // "4 04 16 16"      hour 12/24
    "{0:m mm}",          dt);  // "5 05"            minute
    "{0:s ss}",          dt);  // "7 07"            second
    "{0:f ff fff ffff}", dt);  // "1 12 123 1230"   sec.fraction
    "{0:F FF FFF FFFF}", dt);  // "1 12 123 123"    without zeroes
    "{0:t tt}",          dt);  // "P PM"            A.M. or P.M.
    "{0:z zz zzz}",      dt);  // "-6 -06 -06:00"   time zone
