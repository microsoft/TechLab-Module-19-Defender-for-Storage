@lab.Title

**Please enter your own Microsoft alias (without the @microsoft.com) in the field below before starting the lab**. This information is required to correctly associate your activity with your learner record and ensure your completion is accurately captured and reported. For data integrity and compliance reasons, learners may only enter their own alias.   After completing the lab, please allow up to 5 business days for all reporting systems to fully reflect your completion.

@lab.ActivityGroup(aliascapture)

===


## Survey

@lab.ActivityGroup(initialsurvey)

===

## Objectives

In these exercises, you will learn how to enable Defender for Storage and leverage its capabilities.

## Table of Contents

* Task 01: Prepare the environment for a Defender for Storage Plan.
* Task 02: Upload malware to a Storage Account.
* Task 03: Security alert.
* Task 04: Configure automation to delete the malicious file.
* Task 05: Code to upload files to a storage account and monitor the Blob Index tag.
* Task 06: Set up "Send Scan Results to Log Analytics" and Read It.
* Task 07: Function App based on Grid Events.
* Task 08: ABAC for users not to read malicious files.
* Task 09: Configure and Test On-Demand Malware Scanning.
* Task 10: Observe results in Log Analytics.
* Task 11: Test on-demand malware scanning.
* Task 12: Test on-demand scanning via API.

---

⌛ Estimated time to complete this lab: **60 minutes**

===


## Using this Lab

>[!hint] **Copy Text Supported** 
>  
> The fill in fields of this simulation require the exact text be entered to progress. To make that easier, you can select ++Copy Text++ options in the instructions pane to copy directly into your simulation text entry fields.


---

###**Images and diagrams**   

All images and diagrams in the lab instructions are selectable. Selecting any image opens a zoomed view in a separate window for better clarity and analysis. 

---

###**Split Window feature**   

If you're equipped with multiple screens, you can use the **Split Window** feature to place the lab instructions on a separate screen, making better use of your screen real estate.  


To enable this feature:   

1. Go to the **gear** ![68ixtli3.png](instructions346090/68ixtli3.png)icon in the upper-right corner of the instructions pane.   

1. On the lower side of the **Settings** pane, select **Split Windows**.

![ce7v4jbf.png](instructions346090/ce7v4jbf.png)



===

## Task 01: Preparing the environment for a Defender for Storage plan

1. In the Azure portal dashboard select **Microsoft Defender for Cloud**.



	![qu0thbbu.png](../../media/qu0thbbu.png)

1. In the left side pane, select **Management**, then **Environment settings**.


1. On the lower side of the page, select **Expand all**.



	![wuc4sw46.png](../../media/wuc4sw46.png)

1. Select the **TechMaster-lod52451385** subscription.



	![iamx2nk1.png](../../media/iamx2nk1.png)

1. Under the **Cloud Workload Protection (CWPP)** section, turn on **Storage**. 



	![ynktsn78.png](../../media/ynktsn78.png)

1. Under the **Monitoring coverage** column, select **Settings**.



	![w1h5ntya.png](../../media/w1h5ntya.png)

1. On the **Malware scanning** line, under **Configuration**, select **Edit configuration**.


1. In the flyout pane, select **Soft delete malicious blobs**, then select **Apply**.



	![j88jn5r1.png](../../media/j88jn5r1.png)

1. In the upper-left corner of the page, select **Continue**.



	![s5fird8e.png](../../media/s5fird8e.png)

1. At the top of the page, select **Save**. 



	![11q2gn98.png](../../media/11q2gn98.png)

---

Now all your existing and upcoming Azure Storage Accounts are protected.

===

## Task 02: Upload sample malware to a storage account

A sample malicious test file (EICAR) has already been added to your lab VM for testing purposes. Your lab was also predeployed with a storage account and a log analytics workspace.

>[!knowledge] By default, when you create a storage account, you get the **User Access Administrator** and **Service Administrator** roles. To enable and configure malware scanning, you must have **Owner** roles (such as **Subscription Owner** or **Storage Account Owner**) or specific roles with the necessary data actions.
>
>Learn more about the [**required permissions**](https://learn.microsoft.com/en-us/azure/defender-for-cloud/support-matrix-defender-for-storage).

1. In Azure's search bar, type ++defsto61155713++, press Enter, then select the storage account.


1. In the storage account's left side pane, select **Data storage**, then **Containers**.


1. On the top bar, select **Upload** ![6qsb39y0.png](../../media/6qsb39y0.png).


1. In the flyout pane:


1. Select **Browse for files**.


1. From `C:\Lab Files`, select **eicar**, then select **Open**.



    	![6zc2eyx4.png](../../media/6zc2eyx4.png)

1. In the **Select an existing container** dropdown menu, select **contosofinance**.



        ![wj7un1ym.png](../../media/wj7un1ym.png)

1. Select **Upload**.


1. Select the **contosofinance** container.


1. Above the table, select the right side dropdown menu, then select **Show active and deleted blobs**.



	![5lsngp58.png](../../media/5lsngp58.png)

1. Select the **eicar.com** file you uploaded, which was automatically detected and deleted. Observe the results.


1. Explore the other two tabs, **Versions** and **Snapshots**.



	![clkffv69.png](../../media/clkffv69.png)

===

## Task 03: Assign your user account IAM role

A later task will require the Storage Blob Data Owner role. Let's set that up while you're here.

1. In the upper-left corner of the page, select the **defsto61155713 | Containers** breadcrumb link.



	![gm2n9anp.png](../../media/gm2n9anp.png)

1. In the storage account's left side pane, select **Access Control (IAM)**.


1. Select **Add role assignment**.



	![6x83ajtl.png](../../media/6x83ajtl.png)

1. In the search box above the table, type ++Storage Blob Data Owner++ and press Enter, then select the result in the list.



	![9jvtg8j3.png](../../media/9jvtg8j3.png)

1. On the lower part of the page, select **Next**.


1. On the line for **Members**, choose **Select members**.


1. In the flyout pane:


1. Type the user and press **Enter**: 


    
    	++User1-61155713@LODSPRODMCA.onmicrosoft.com++

1. Choose **Select**.



    	![dybnsxak.png](../../media/dybnsxak.png)

1. On the lower side of the page, select **Review + assign** twice.



===

## Task 04: Security alerts

>[!alert] In a real environmnet, you may need to wait 24 hours before proceeding.

1. In the top search bar, type ++Microsoft Defender for Cloud++ and press **Enter**, then select the result.



	![grhp3rbw.png](../../media/grhp3rbw.png)

1. In the left side pane, under **General**, select **Security alerts**.


1. Select the **Malicious blob uploaded...** alert.



	![2t1mzwlr.png](../../media/2t1mzwlr.png)

1. Review the details in the flyout pane, then select **View full details** on the lower side.



	![hsiu29ok.png](../../media/hsiu29ok.png)

1. The security alert contains details and context about the file, the malware type, and recommended investigation and remediation steps.



	![i11echup.png](../../media/i11echup.png)

1. From the **Related entities**, select first **Azure resource**, **Blob** and then **Malware** to find more details about this attack.



===

## Task 05: Configure automation to delete the malicious file based on security alert

You'll setup a workflow automation using a Logic App to remove malicious files when a specific security alert is triggered.

1. In the upper-left corner of the page, select the **Microsoft Defender for Cloud | Security alerts** breadcrumb link.



	![lwadge51.png](../../media/lwadge51.png)

1. In the left side pane, select **Management**, then **Workflow automation**.


1. On the top bar, select **+ Add workflow automation**.



	![5i1besad.png](../../media/5i1besad.png)

1. In the flyout pane, enter the following details:



    | Item | Value |
    |:---------|:---------|
    | Name | ++delete-malicious-blob++ |
    | Resource group | **ResourceGroup1** |
    | Alert name contains | ++Malicious blob uploaded to storage account++ |
    | Logic App name | **Remove-MalwareBlob** |

	![kervj225.png](../../media/kervj225.png)

1. On the lower side of the pane, select **Create**.



	![y2akvmv5.png](../../media/y2akvmv5.png)

===

## Task 06: Code to upload files to storage account and monitor the blob index tag itself

With this Python code you'll be able to create a benign file and an EICAR test file that will be uploaded to your storage account. The results will be surfaced in your IDE.

1. On the VM's task bar, open **Visual Studio Code**.



	>[!note] This will automatically open your lab's project folder: 
    >
    >`C:\Lab Files`

1. Select **File**, then **New Text File**.


1. Right-click anywhere on the new file content area.



	>[!hint] The code below is already in the clipboard, you **DO NOT** need to copy it again.

    
python
    from azure.identity import DefaultAzureCredential
    from azure.storage.blob import BlobClient
    from azure.core.exceptions import ResourceNotFoundError
    import time

    credential = DefaultAzureCredential()

    # Information about our storage account that we will be uploading files to.  
    storage_url ="https://defsto@lab.LabInstance.Id.blob.core.windows.net" # CHANGE THIS.
    container = "contosofinance"                          # CHANGE THIS.

    # Info and data for our example of non malware
    file1 = "ContosoSecretRecipe.txt"
    file1Content = b"The quick brown fox jumps over the lazy dog."

    # Info and data for our example of malware (Added double backslash for \P to fix the SyntaxWarning)
    file2 = "TotallyNotMalware.txt"
    file2Content = b"X5O!P%@AP[4\\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*" 

    files = [
        (file1, file1Content), 
        (file2, file2Content)
    ]

    def get_blob_client(blob_name) -> BlobClient:
        return BlobClient(
            account_url=storage_url,
            container_name=container,
            blob_name=blob_name,
            credential=credential
        )

    # You can do better error handling here if you'd like
    def do_we_trust(tags:dict) -> bool:
        match tags['Malware Scanning scan result']:
            case 'No threats found':
                return True
            case _:
                return False
                
    def main(files:list):
        for file in files:
            # Get a blob client
            blob_client = get_blob_client(file[0])
            # Write to our blob
            uploadReturn = blob_client.upload_blob(data=file[1], overwrite=True)
            
            try:
                # Check the tags to see our antimalware scan results tag
                tags = blob_client.get_blob_tags()
                while True:
                    if 'Malware Scanning scan result' in tags.keys():
                        symbol = '\u2714' if do_we_trust(tags) else '\u2716'
                        break
                    else: 
                        time.sleep(1)
                        tags = blob_client.get_blob_tags()
                
                # Let's look at the results
                print(f"{file[0]} was uploaded to: {storage_url}/{container}: {symbol}")
                print(f"    etag: {uploadReturn['etag']}")
                print(f"    last_modified: {uploadReturn['last_modified']}")
                print(f"    tags: {tags}")
                print()
                
            except ResourceNotFoundError:
                # If the blob is gone, Defender or the Logic App already deleted it
                print(f"{file[0]} was uploaded to: {storage_url}/{container}: \u2716")
                print(f"    etag: {uploadReturn['etag']}")
                print(f"    last_modified: {uploadReturn['last_modified']}")
                print(f"    tags: [Blob not found. It was likely deleted by Defender Automated Remediation!]")
                print()
                
    if __name__ == "__main__":
        main(files)
    ```

    >[!hint] This incorporates the values of your storage account URL and **contosofinance** container.

1. Select **Paste** from the context menu.


1. Select **File**, then **Save** twice. This will save it as `antimalware.py`.


1. On VS Code's top bar, select **Terminal**, then **New Terminal**.



    > [!note] The following Python packages have already been installed:
    > - **azure-common**
    > - **azure-core**
    > - **azure-identity**
    > - **azure-storage-blob**

1. In the bottom terminal pane, paste the following to sign in to your Azure tenant, then press **Enter**:



	++Connect-AzAccount++

1. In the sign in dialog, select **Continue**.


1. Select **No, this app only**.


1. In the VS Code terminal, paste the following command, then press **Enter**:



	++python ./antimalware.py++

	![qf20zvz4.png](../../media/qf20zvz4.png)

    >[!note] In the results you'll have two files: 
    > - **ContosoSecretRecipe.txt**
    > - **TotallyNotMalware.txt**
    >
    >Both files were declared in your code. The first file was a benign one so it shows a checkmark (✔) next to its path. 
    >
    >The second file was an EICAR antivirus test file that the malware scanning identifies as malicious. This one displays (✖) next to its path. 
    >
    >In the results, you'll also see values like **etag**, **last_modified**, and the blob index **tags**, as well as the time when the scan was performed.

===

## Task 07: Send scan results to Log Analytics and an Event Grid topic

>[!knowledge] Malware Scanning error messages were updated in August 2025. For more information visit this [blog post](https://techcommunity.microsoft.com/blog/microsoftdefendercloudblog/defender-for-storage-malware-scan-error-message-update/4436304).

1. In the system tray, select the Microsoft Edge browser icon.


1. In Azure's search box, type ++defsto61155713++ and press **Enter**. Then from the results, select the storage account.


1. In the left side pane, go to **Security + networking**, then select **Microsoft Defender for Cloud**.


1. Under the top **Microsoft Defender for Storage** section, select **Settings**.



	![8twb2qkd.png](../../media/8twb2qkd.png)

1. In the flyout pane:


1. Turn on **Override Defender for Storage subscription-level settings**.



    	![ys4jr334.png](../../media/ys4jr334.png)

        >[!knowledge] Use this to set configurations that are different from the subscription. This also allows you to disable Defender for Storage on the storage account.

1. Clear the checkbox for **Soft delete malicious blobs**.


    
    	>[!knowledge] This is the setting that previously deleted the EICAR file from the container, which your custom automation now handles.

1. Select the checkbox for **Send scan results to Event-Grid topic**.


1. In the dropdown menu of the same line, select the **egt-malware-scans-61155713** topic.



    	>[!note] You'll setup a Function App based on Event Grid events in a later task.

1. Select the checkbox for **Send scan results to Log Analytics**.


1. In the dropdown menu of the same line, select the **def-la-61155713** Log Analytics workspace.



    	![lh7sc4fj.png](../../media/lh7sc4fj.png)

1. On the lower side of the pane, select **Save**.



===

## Task 08: Function App based on Event Grid events

In this exercise you'll use an Azure Function App based on Event Grid events. The Azure Function code is going to help you move a malicious blob from the container where you are uploading files, to a different container (quarantine). The Event Grid events come from the Malware Scanning scan results.

>[!hint] A Function App was predeployed to your environment with the **Storage Blob Data Contributor** role assigned at the **Resource Group** level.

1. In Azure's search box, type ++Remove-MalwareBlob++, press **Enter**, then select this logic app.


1. On the top bar, select **Disable**. ![v3pfpvua.png](../../media/v3pfpvua.png)



	>[!note] Your function app will take the suspected malware and move it to a separate container rather than delete it.

1. Go back to your Visual Studio Code window from the taskbar.



	![vwqtedkb.png](../../media/vwqtedkb.png)

1. In the top search box:


1. Type ++Azure Functions: Create Function++, press **Enter**, then select it.



		![qc4azwe9.png](../../media/qc4azwe9.png)

1. Select **Browse**.


1. From `C:\Lab Files`, select **DefenderRemediationFunction**, then choose **Select**.



    	![sj9cu1zn.png](../../media/sj9cu1zn.png)

1. Select **C#**.


1. Select **.NET 8.0**.


1. Select **Azure Blob Storage trigger**.


1. For **function name**, type ++Company.MoveMaliciousBlob++ and press **Enter**.


1. Select **Create new local app setting**.


1. Select **Sign in to Azure**.


1. In the dialog, select **Next**.


1. Select **No, this app only**.


1. In the top search box dropdown menu:


1. Select the **defsto61155713** storage account.


1. Type ++contosofinance++ and press **Enter**.



		![kjbrx8ue.png](../../media/kjbrx8ue.png)

	>[!note] This will setup your new project folder with some base files.

1. Right-click anywhere on the content area of the file and select **Paste**. You'll replace all the content with the text below. 



    >[!hint] This text is already in your clipboard, **NO NEED** to copy it again.

    ```
    using Azure;
    using Azure.Identity;
    using Azure.Messaging.EventGrid;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    using Microsoft.Azure.Functions.Worker;
    using Microsoft.Extensions.Logging;
    using System.Text.Json;

    namespace Company.MoveMaliciousBlob
    {
        public class MoveMaliciousBlob
        {
            private readonly ILogger _logger;
            private const string AntimalwareScanEventType = "Microsoft.Security.MalwareScanningResult";
            private const string MaliciousVerdict = "Malicious";
            private const string MalwareContainer = "malware";
            private const string InterestedContainer = "contosofinance";

            public MoveMaliciousBlob(ILoggerFactory loggerFactory)
            {
                _logger = loggerFactory.CreateLogger<MoveMaliciousBlob>();
            }

            [Function("MoveMaliciousBlob")]
            public async Task Run([EventGridTrigger] EventGridEvent eventGridEvent)
            {
                if (eventGridEvent.EventType != AntimalwareScanEventType)
                {
                    _logger.LogInformation("Event type is not a Malware Scanning result. Skipping.");
                    return;
                }

                var eventData = JsonDocument.Parse(eventGridEvent.Data).RootElement;
                var verdict = eventData.GetProperty("scanResultType").GetString();
                var blobUriString = eventData.GetProperty("blobUri").GetString();
                var blobETag = new ETag(eventData.GetProperty("eTag").GetString());

                var blobUri = new Uri(blobUriString!);
                var blobUriBuilder = new BlobUriBuilder(blobUri);

                if (blobUriBuilder.BlobContainerName != InterestedContainer) return;

                if (verdict == MaliciousVerdict)
                {
                    _logger.LogWarning("Malicious blob detected: {0}. Quarantining...", blobUri);
                    await MoveBlobAsync(blobUri, blobETag, MalwareContainer);
                }
            }

            private async Task MoveBlobAsync(Uri blobUri, ETag blobETag, string destContainerName)
            {
                var uriBuilder = new BlobUriBuilder(blobUri);
                var destContainerUri = new Uri($"https://{uriBuilder.Host}/{destContainerName}");
                
                var credential = new DefaultAzureCredential();
                var srcClient = new BlobClient(blobUri, credential);
                var destContainerClient = new BlobContainerClient(destContainerUri, credential);

                await destContainerClient.CreateIfNotExistsAsync();
                var destClient = destContainerClient.GetBlobClient(uriBuilder.BlobName);

                // Copy then delete (Move)
                var copyOp = await destClient.StartCopyFromUriAsync(srcClient.Uri, new BlobCopyFromUriOptions { 
                    SourceConditions = new BlobRequestConditions { IfMatch = blobETag } 
                });
                await copyOp.WaitForCompletionAsync();
                await srcClient.DeleteAsync();
                
                _logger.LogInformation("Blob moved to {0} successfully.", destContainerName);
            }
        }
    }
    ```

	![ort6y85g.png](../../media/ort6y85g.png)

	>[!note] On lines 17 and 18, you'll see the **contosofinance** is setup as the container to scan. It'll then route potential malware to the **malware** container.

1. Open the **local.settings.json** file.



	![n39eyaoe.png](../../media/n39eyaoe.png)

1. Copy the value of **defsto61155713_STORAGE**.



	![2i8alg1y.png](../../media/2i8alg1y.png)

1. Right-click on the empty space next to **AzureWebJobsStorage**, then select **Paste** in the context menu.



	![672dvvqs.png](../../media/672dvvqs.png)

1. From the upper menu bar, select **File**, then **Save All**.


1. In VS Code's menu bar, select **Terminal**, then **New Terminal**.


1. In the lower terminal pane, enter the following command and then press **Enter**:



	++dotnet add package Azure.Identity++

	>[!note] In a real environment you might need to install other packages as well.
    > `dotnet nuget add source https://api.nuget.org/v3/index.json -n nuget.org`
    > `dotnet add package Azure.Messaging.EventGrid`
    > `dotnet add package Azure.Storage.Blobs`
    > `dotnet add package Microsoft.Azure.Functions.Worker.Extensions.EventGrid`
    > `dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs`

1. Verify the project builds successfully by entering the following:



	++dotnet build++

	![c1ph5hi5.png](../../media/c1ph5hi5.png)

1. In VS Code's command bar, select ++Azure Functions: Deploy to Function App++.


1. Select the predeployed **func-malware-61155713** app.



	![zzqjlvjs.png](../../media/zzqjlvjs.png)

1. In the VS Code dialog, select **Deploy**.


1. The deployment status appears in the bottom pane when deployment finishes.



	![7tnic1bq.png](../../media/7tnic1bq.png)

    >[!alert] In a real environment, this may take a couple of minutes to complete.

1. Go back to Microsoft Edge.


1. In Azure's search box, type ++egt-malware-scans-61155713++, press **Enter** then select this Event Grid Topic.



	![5lldrw4w.png](../../media/5lldrw4w.png)

1. In the left side pane, select **Entities**, then **Event Subscriptions**.


1. On the top bar, select **+ Event Subscription**.



	![eb23dwh8.png](../../media/eb23dwh8.png)

1. Enter the following details:



    | Item | Value |
    |:---------|:---------|
    | Name | ++malwareEventSubscription++ |
    | Endpoint Type | **Azure Function** |

	![xo4gsdes.png](../../media/xo4gsdes.png)

1. On the line for **Endpoint**, select **Configure an endpoint**.


1. On the lower side of the flyout pane, select **Confirm Selection**.



	![fbwcvmog.png](../../media/fbwcvmog.png)

1. In the lower-left corner of the page, select **Create**.


1. On the top bar, select **+Event Subscription** again. 


1. Enter the following details:



    | Item | Value |
    |:---------|:---------|
    | Name | ++malwareQueue++ |
    | Endpoint Type | **Storage Queue** |

    ![vqvdcuzy.png](../../media/vqvdcuzy.png)

1. On the line for **Endpoint**, select **Configure an endpoint**.


1. In the flyout pane:


1. Enter the following details, then select **Create**:



        | Item | Value |
        |:---------|:---------|
        | Storage account | **defsto61155713** |
        | Queue | **Create new queue** |
        | Queue name | ++malevents++ |

    	![gkshqjyk.png](../../media/gkshqjyk.png)

1. In the lower-left corner of the page, select **Create**.



	>[!note] **malwareQueue** will receive all the events when they're triggered.

1. In Azure's top search box, type ++defsto61155713++, press **Enter**, then select the storage account.


1. In the left side pane, select **Data storage**, then **Containers**.


1. On the upper action bar, select **Upload**.


1. In the flyout pane:


1. Select **Browse for files**.


1. From `C:\Lab Files`, **eicar** is selected. Select **Open**.



    	![2phwk5vq.png](../../media/2phwk5vq.png)

1. In the **Select an existing container** dropdown menu, select **contosofinance**.


1. Select **Upload**.


1. In the left side pane, under **Data storage**, select **Queues**.


1. Select the **malevents** queue.



	![k6y8goo9.png](../../media/k6y8goo9.png)

1. Observe that the **Overview** page displays a list of events on the storage account.



	![yo8tx9pb.png](../../media/yo8tx9pb.png)

1. In the upper-left corner of the page, select the **defsto61155713 | Queues** breadcrumb link.


1. In the left side pane, under **Data storage**, select **Containers**.


1. Select the **malware** container.



	>[!note] Observe the **eicar.com** file was automatically moved by the function app.
    >
    >![76qnt1mm.png](../../media/76qnt1mm.png)

1. In Azure's search box, type ++egt-malware-scans-61155713++ and press **Enter**, then select the Event Grid Topic.


1. In the left side pane, under **Entities**, select **Event Subscriptions**.


1. Select **malwareQueue**.



	![6pw1go7b.png](../../media/6pw1go7b.png)

	>[!alert] In a real environment, it may take a few minutes to see the latest events.

===

## Task 09: ABAC for users not to read malicious files

To make sure that your apps and users can only read non-malicious files, which means that Defender for Storage found without threats, you can implement Attribute-Based Access Control (ABAC). In this exercise you'll explore how you can have roles that have a condition to only read the files that have no threats found.

1. In Azure's search box, type ++defsto61155713++, press **Enter**, then select the storage account.


1. In the left side pane, select **Access Control (IAM)**.


1. Select **Add role assignment**.


1. In the search box above the table, type ++Storage Blob Data Contributor++ and press Enter.


1. Select the **Storage Blob Data Contributor** result.


1. On the lower side of the page, select **Next**.


1. On the line for **Members**, choose **Select members**.


1. In the flyout pane:


1. Type your user account, and press **Enter**: 


    
    	++User1-61155713@LODSPRODMCA.onmicrosoft.com++

1. Select the result.


1. On the lower side of the pane, choose **Select**.



    	![v90f0o5e.png](../../media/v90f0o5e.png)

1. On the lower side of the page, select **Next**.


1. Select **Add condition**.


1. Under the **Add action** section, select **Add action**.



	![hy4msbn6.png](../../media/hy4msbn6.png)

1. In the flyout pane:


1. Select the checkbox for **Read a blob**.



    	>[!knowledge] Blobs are passive data and can't execute within Azure Storage. Security risk only occurs when a user or application **Reads** (downloads) the malicious payload to a local environment where it can be executed. Restricting the **Read** action prevents this transfer.

1. On the lower side of the pane, choose **Select**.



    	![k8iwrk21.png](../../media/k8iwrk21.png)

1. Under the **Build expression** section, select **Add expression**.


1. Enter the following details for the expression:



    | Item | Value |
    |:---------|:---------|
    | Attribute source | **Resource** |
    | Attribute | **Blob index tags [Values in key]** |
    | Key | ++Malware scanning scan result++ |
    | Operator | **StringEqualsIgnoreCase** |
    | Value | ++No threats found++ |

	![9oi0q6bw.png](../../media/9oi0q6bw.png)

1. Move to the top of the page and try changing **Editor type** to **Code**.



	![odxwtisg.png](../../media/odxwtisg.png)

    >[!knowledge] The **Code** editor is highly efficient for auditing, duplicating, or scaling complex conditions across multiple roles. 
    >
    >Notice the logic explicitly allows **Listing** (so users can see the files exist in the UI), but strictly gates the actual **Read** action. The file content remains inaccessible unless the **Malware scanning scan result** index tag matches the **No threats found** string, creating an automated "clean-room" access policy.

1. In the lower-left corner of the page, select **Save**.


1. In the lower-left corner of the page, select **Review + assign** twice.



	>[!note] You previously granted your account a higher level permission that supercedes this, but this is for general knowledge.


===

## Task 10: Observe results in Log Analytics

Reupload the EICAR file you uploaded in Task 02, then observe the results in Log Analytics.

1. In the left side pane, under **Data storage**, select **Containers**.


1. On the top bar, select **Upload**.


1. In the flyout pane:


1. Select **Browse for files**.


1. From `C:\Lab Files`, **eicar** is selected. Select **Open**.



    	![w63qqj4m.png](../../media/w63qqj4m.png)

1. In the **Select an existing container** dropdown menu, select **contosofinance**.


1. Select **Upload**.


1. In Azure's search box, type ++def-la-61155713++, press **Enter**, then select this Log Analytics workspace.


1. In the left side pane, select **Logs**.


1. Near the upper-right corner of the page, select the **Simple mode** dropdown menu, then select **KQL mode**.



	![ywox204i.png](../../media/ywox204i.png)

1. In the query editor, right-click and select **Paste** in the context menu. This will add the below command.



    
KQL
    StorageMalwareScanningResults 
    | sort by TimeGenerated asc
    ```

1. On the bar above the editor, select **Run**.



	![20i993f6.png](../../media/20i993f6.png)

1. In the bottom **Results** pane, expand the first entry under the **TimeGenerated** column and observe the results.



	![h4uvr3ob.png](../../media/h4uvr3ob.png)

===

## Task 11: Test on-demand malware scanning

1. In the search bar, type +++defsto61155713+++, press **Enter** and select the storga account.


1. In the left side pane, select **Security + networking**, then **Microsoft Defender for Cloud**.


1. Under the **On-demand malware scanning** section, select **Scan storage account for malware**.



	![zhm20al3.png](../../media/zhm20al3.png)

1. Observe the results.



	![b1nb2xjm.png](../../media/b1nb2xjm.png)

	>[!knowledge] The cost estimate is based on metrics which are updated every few hours. If the storage account was previously empty, it can show a wrong estimate until its next update.

===

## Task 12: Testing on-demand scanning via API

The following task uses the [On Demand Insomnia](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Files/On_Demand_Insomnia_2024-10-14.yaml) collection, which hosts the following APIs:
- **Get Scan**
- **Start Scan**
- **Cancel Scan**

1. From the system taskbar, select the **VS Code** icon.



	![9bkwxrcv.png](../../media/9bkwxrcv.png)

1. On VS Code's top bar, select **Terminal**, then **New Terminal**.


1. In the terminal pane, type the following to sign in to your Azure tenant, then press **Enter**:



	++Connect-AzAccount -AuthScope https://management.azure.com++

1. In the VS Code terminal, enter the following to retriever your account's Bearer token, then press **Enter**:



    ++[System.Net.NetworkCredential]::new("", $secureToken).Password++

   

    ![zheyf2j8.png](../../media/zheyf2j8.png)

	>[!note] In a real environmnet, you'd need to copy and paste the entire token in a text editor like Notepad. 
	>
	> ![1b36xc0z.png](../../media/1b36xc0z.png)
	>
    > This value will be needed in a later step.

1. On the VM's taskbar, open Insomnia.



	![8uzs1ug7.png](../../media/8uzs1ug7.png)

1. Select **Continue**.



	![h7shjdr5.png](../../media/h7shjdr5.png)

1. At the top of the left pane, select **Scratch pad**, then select **Import**.



	![ec5wxxey.png](../../media/ec5wxxey.png)

1. In the dialog:


1. Select **Choose Files**.



        ![1bbouauo.png](../../media/1bbouauo.png)

1. Go to `C:\Lab Files`, select **On_Demand_Insomnia_2024-10-14**, then select **Open**.



        ![2igv2eza.png](../../media/2igv2eza.png)

1. Select **Import**.



    	![jrugo546.png](../../media/jrugo546.png)

1. Near the top of the left pane, select the **Collection** tab.



	![iu35oki0.png](../../media/iu35oki0.png)

1. In the left pane, select **Base Environment**, then select the edit (![8k66ykyd.png](../../media/8k66ykyd.png)) icon on the line for **Collection Environments**.



	![o589dopm.png](../../media/o589dopm.png)

    >[!note] In a real environment, you would need to replace the variables with the following:
	>
    >| Item | Value |
    >|:---------|:---------|
    >| endpoint | `management.azure.com` |
    >| subscriptionId | [your subscription ID] |
    >| resourceGroup | [your resource group] |
    >| storageAccountName | [your storage account name] |
    >| settingsName | **current** |
    >| bearerToken | [the token you've copied from the previous steps] |
    >| apiVersion | **2024-10-01-preview** |
	>
    > ![r3k1u1r9.png](../../media/r3k1u1r9.png)

1. In the lower-right corner of the pane, select **Close**. 


1. In the left pane, select the **Start Scan** POST request.



	![5xjgptua.png](../../media/5xjgptua.png)

1. In the middle pane, select the **Auth** tab.


	
    ![xpplyjh3.png](../../media/xpplyjh3.png)

	>[!note] This uses the **bearerToken** variable you just updated to authenticate.

1. Select **Send**, and observe the results in the rightmost pane.



	![lzjaol7v.png](../../media/lzjaol7v.png)

---

### Get Scan

1. In the left pane, select the **Get Scan** request.


1. Select **Send**.



	![osifpp1c.png](../../media/osifpp1c.png)

>[!knowledge] The **Cancel Scan** request does what you expect and cancels a malware scan in progress.

=== 
>[!Alert] **IMPORTANT:** These labs are hosted on the Skillable platform. Completion data is collected and then exported to Success Factors every Monday. SF require another 1-3 days to process that data. The status for this lab will be visible in Viva and Learning Path next week. 
>
Be sure to select "**Submit**" in the bottom right corner to get credit for completing this lab. 

@lab.ActivityGroup(completionsurvey)

>[!Alert] After answering the survey questions, select **submit** to complete and end the lab. **This is required in order to receive credit for lab completion**.




