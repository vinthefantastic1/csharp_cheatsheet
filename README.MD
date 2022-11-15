### CSI - CSharp Interactive:
    https://learn.microsoft.com/en-us/archive/msdn-magazine/2016/january/essential-net-csharp-scripting

        C:\Program Files (x86)\Microsoft Visual Studio 14.0>csi
        Microsoft (R) Visual C# Interactive Compiler version 1.1.0.51014
        Copyright (C) Microsoft Corporation. All rights reserved.
        Type "#help" for more information.
        > System.Console.WriteLine("Hello! My name is Inigo Montoya");
        Hello! My name is Inigo Montoya
        > 
        > ConsoleColor originalConsoleColor  = Console.ForegroundColor;
        > try{
        .  Console.ForegroundColor = ConsoleColor.Red;
        .  Console.WriteLine("You killed my father. Prepare to die.");
        . }
        . finally
        . {
        .  Console.ForegroundColor = originalConsoleColor;
        . }
        You killed my father. Prepare to die.
        > IEnumerable<Process> processes = Process.GetProcesses();
        > using System.Collections.Generic;
        > processes.Where(process => process.ProcessName.StartsWith("c") ).
        .  Select(process => process.ProcessName ).Distinct()
        DistinctIterator { "chrome", "csi", "cmd", "conhost", "csrss" }
        > processes.First(process => process.ProcessName == "csi" ).MainModule.FileName
        "C:\\Program Files (x86)\\MSBuild\\14.0\\bin\\csi.exe"
        > $"The current directory is { Environment.CurrentDirectory }."
        "The current directory is C:\\Program Files (x86)\\Microsoft Visual Studio 14.0."
        >

### Winforms get deployment version
    if (ApplicationDeployment.IsNetworkDeployed) 
    {
        var v = $"{ApplicationDeployment.CurrentDeployment.CurrentVersion}";
    }

### Get app.config values
    var networkPath = Properties.Settings.Default.networkPath;

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
    
### Sum of a datatable column
    var sum = dt.Compute("Sum(Amount)", dt.DefaultView.RowFilter);
 
### Numbers
    {0:C2}
    {12345:N2}
    
    decimal val2 = 12345.67;
    Console.WriteLine($"The number is {val2,10:N2}"); // Displays "The number is  12,345.67"

    

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

### EF Query to Class Instance

            var data = db.GCS_Chargeback_Summary.Where(i => i.serviceType == serviceType & i.status == status).
                    Select(c => new JobListing()
                    {
                        jobNo = c.jobNo,
                        totalCost = c.totalCharges,
                        description = c.description,
                        WBS = c.wbs,
                        CC = c.cc,
                        IO = c.io,
                        status = c.status,
                        postingDate = c.postingDate,
                        SapMessage = c.SAP_Message,
                        CreateDate = c.createDate,
                        SAPDocuNum = c.SAP_Doc_No,
                        SAPJobNo = c.SAP_Job_No,
                        ServiceType = c.serviceType


                    });

            var datalist = data.ToList();

### Return a SCALAR value in C# Dataset

Update the Dataset to return the last updated recordid for a datatable.update() call:
1) Right click the table adapter,
2) Choose Query
3) USE SQL
4) down at the bottom choose INSERT
5) Enter your query like below: (notice the SELECT using SCOPE_IDENTITY() after the INSERT)
         
        INSERT INTO [dbo].[bank_update_requests] ([request_version], [vendor_id], [stc_upi], [vendor_type], [request_type], [request_type_descr], 
        [bank_type], [payment_type], [country_code], [currency_code], [bene_name], [bank_key], [account_number], [IBN_number], [swift_code], 
        [ABA_number], [bank_name], [request_status], [request_status_descr], [submit_date], [submit_time], [status_updatedate], [status_updatetime], 
        [completion_date], [completion_time], [Routing_IRCCode], [From_acct_No], [From_bank_key], [From_bank_cntkey], [IBANK_type], [IBANK_swift_code], 
        [IBANK_account], [IBANK_name], [IBANK_key], [IBANK_Country], [IBANK_status], [Requester_Comment], [Requester_Comment_2], [vmr_comment], 
        [vmr_comment_2], [vmr_comment_3], [vmr_comment_4], [TTL_UPI], [ADMIN_UPI], [TAX_ID], [BANK_TAX_ID], [CITAD_CODE], [IFSC_CODE], [SORT_CODE], 
        [BRANCH_CODE], [PURPOSE_CODE], [BSB_NO], [BANK_CODE], [KBA_CODE], [EKNP_CODE], [PAYMT_PURPOSE], [USD_PAY], [CPF_CODE], [TRANSIT_CODE], [CBU_CODE], 
        [BIK_CODE], [VO_CODE], [ROUTING_NO], [SKN_CODE], [DOB], [CNIC], [BEN_ADDRESS], [BENE_STATE], [REGION], [BUILDING_CODE], [POSTAL_CODE], 
        [STREET_NAME], [PHONE_NO], [EMAIL], [misc_1], [misc_2], [misc_3], [misc_4], [From_IBANK_account], [From_IBANK_key], [From_IBANK_Country],
        [CLABE_NO], [BBAN], [CCI], [ACC_TYPE]) VALUES (@request_version, @vendor_id, @stc_upi, @vendor_type, @request_type, @request_type_descr,
        @bank_type, @payment_type, @country_code, @currency_code, @bene_name, @bank_key, @account_number, @IBN_number, @swift_code, @ABA_number,
        @bank_name, @request_status, @request_status_descr, @submit_date, @submit_time, @status_updatedate, @status_updatetime, @completion_date,
        @completion_time, @Routing_IRCCode, @From_acct_No, @From_bank_key, @From_bank_cntkey, @IBANK_type, @IBANK_swift_code, @IBANK_account, 
        @IBANK_name, @IBANK_key, @IBANK_Country, @IBANK_status, @Requester_Comment, @Requester_Comment_2, @vmr_comment, @vmr_comment_2, @vmr_comment_3, 
        @vmr_comment_4, @TTL_UPI, @ADMIN_UPI, @TAX_ID, @BANK_TAX_ID, @CITAD_CODE, @IFSC_CODE, @SORT_CODE, @BRANCH_CODE, @PURPOSE_CODE, @BSB_NO, 
        @BANK_CODE, @KBA_CODE, @EKNP_CODE, @PAYMT_PURPOSE, @USD_PAY, @CPF_CODE, @TRANSIT_CODE, @CBU_CODE, @BIK_CODE, @VO_CODE, @ROUTING_NO,
        @SKN_CODE, @DOB, @CNIC, @BEN_ADDRESS, @BENE_STATE, @REGION, @BUILDING_CODE, @POSTAL_CODE, @STREET_NAME, @PHONE_NO, @EMAIL, @misc_1,
        @misc_2, @misc_3, @misc_4, @From_IBANK_account, @From_IBANK_key, @From_IBANK_Country, @CLABE_NO, @BBAN, @CCI, @ACC_TYPE); SELECT request_id, 
        request_version, vendor_id, stc_upi, vendor_type, request_type, request_type_descr, bank_type, payment_type, country_code, currency_code,
        bene_name, bank_key, account_number, IBN_number, swift_code, ABA_number, bank_name, request_status, request_status_descr, submit_date, 
        submit_time, status_updatedate, status_updatetime, completion_date, completion_time, Routing_IRCCode, From_acct_No, From_bank_key, 
        From_bank_cntkey, IBANK_type, IBANK_swift_code, IBANK_account, IBANK_name, IBANK_key, IBANK_Country, IBANK_status, Requester_Comment, 
        Requester_Comment_2, vmr_comment, vmr_comment_2, vmr_comment_3, vmr_comment_4, TTL_UPI, ADMIN_UPI, TAX_ID, BANK_TAX_ID, CITAD_CODE, 
        IFSC_CODE, SORT_CODE, BRANCH_CODE, PURPOSE_CODE, BSB_NO, BANK_CODE, KBA_CODE, EKNP_CODE, PAYMT_PURPOSE, USD_PAY, CPF_CODE, TRANSIT_CODE, 
        CBU_CODE, BIK_CODE, VO_CODE, ROUTING_NO, SKN_CODE, DOB, CNIC, BEN_ADDRESS, BENE_STATE, REGION, BUILDING_CODE, POSTAL_CODE, STREET_NAME, 
        PHONE_NO, EMAIL, misc_1, misc_2, misc_3, misc_4, From_IBANK_account, From_IBANK_key, From_IBANK_Country, CLABE_NO, BBAN, CCI, ACC_TYPE 
        FROM bank_update_requests WHERE (request_id = SCOPE_IDENTITY()) AND (request_version = @request_version)

6) ~~CHANGE EXECUTE MODE TO SCALAR (in properties of newly created Query)

### Razor Pages - ActionLink with dynamic 'row' variable and parameters
                        foreach (var row in ViewBag.ItemList)
                        {
                            <tr>
                                                    <td>
 

                                                        @Html.ActionLink((string)row.sku, "Index", "BookSales", new { SearchString = row.sku, BeginDate = ViewBag.TempBeginDate, EndDate = ViewBag.TempEndDate }, new { target = "_blank" })


                                                    </td>

### EF Validation Errors

                db.job_error_email_log.Add(job);
                try
                {
                    db.SaveChanges();
                }
                catch (DbEntityValidationException e)
                {
                    foreach (var eve in e.EntityValidationErrors)
                    {
                        Console.WriteLine("Entity of type \"{0}\" in state \"{1}\" has the following validation errors:",
                            eve.Entry.Entity.GetType().Name, eve.Entry.State);
                        foreach (var ve in eve.ValidationErrors)
                        {
                            Console.WriteLine("- Property: \"{0}\", Error: \"{1}\"",
                                ve.PropertyName, ve.ErrorMessage);
                        }
                    }
                    throw;
                }
