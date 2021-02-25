### Winforms get deployment version
    if (ApplicationDeployment.IsNetworkDeployed) 
    {
        string.Format("Version : {0}", ApplicationDeployment.CurrentDeployment.CurrentVersion.ToString(4));
    }
