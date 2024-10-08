---
layout: post
title: Add custom metadata to Azure blob storage files and search them with Azure
  Search
date: 2018-01-31 20:45:21.000000000 -08:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- programming
tags:
- Azure
- AzureSearch
- blob storage
- cloud
meta:
  _edit_last: '1'
  layout: default
  feature_size: blank
  hide_post_title: default
  unlink_post_title: default
  hide_post_meta: default
  hide_post_date: default
  hide_post_image: default
  unlink_post_image: default
  builder_switch_frontend: '0'
  dsq_thread_id: '6451432950'
author:
  login: jj09
  email: jakub.jedryszek@gmail.com
  display_name: jj09
  first_name: ''
  last_name: ''
permalink: "/add-custom-metadata-to-azure-blob-storage-files-and-search-them-with-azure-search/"
---
<p>Did you know that you can add custom metadata to your blob containers, and even to individual blob files?</p>
<p>You can do it in the <a href="https://portal.azure.com">Azure Portal</a>, using <a href="https://github.com/Azure/azure-storage-net">SDK</a> or <a href="https://docs.microsoft.com/en-us/rest/api/storageservices/set-blob-metadata">REST API</a>.</p>
<p>The most common scenario is adding metadata during file upload. Below code is uploading sample invoice from disk, and adds year, month, and day metadata properties.</p>
{% highlight csharp %}
const string StorageAccountName = "";
const string AccountKey = "";
const string ContainerName = "";

string ConnectionString = $"DefaultEndpointsProtocol=https;AccountName={StorageAccountName};AccountKey={AccountKey};EndpointSuffix=core.windows.net";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(ContainerName);

const string FileName = "Invoice_2017_01_01";
using (var fileStream = System.IO.File.OpenRead($@"D:\dev\BlobMetadataSample\invoices\{FileName}.pdf"))
{
    var fileNameParts = FileName.Split('_');
    var year = fileNameParts[1];
    var month = fileNameParts[2];
    var day = fileNameParts[3];

    var blob = container.GetBlockBlobReference(FileName);
    blob.Metadata.Add("year", year);
    blob.Metadata.Add("month", month);
    blob.Metadata.Add("day", day);
    blob.UploadFromStream(fileStream);

    var yearFromBlob = blob.Metadata.FirstOrDefault(x => x.Key == "year").Value;
    var monthFromBlob = blob.Metadata.FirstOrDefault(x => x.Key == "month").Value;
    var dayFromBlob = blob.Metadata.FirstOrDefault(x => x.Key == "day").Value;

    Console.WriteLine($"{blob.Name} ({yearFromBlob}-{monthFromBlob}-{dayFromBlob})");
}
{% endhighlight %}

<p>If you just want to add metadata to existing blob, instead of calling <code>blob.UploadFromStream(fileStream)</code> you can run <code>blob.SetMetadata()</code>.</p>
<p>When you create new <a href="https://docs.microsoft.com/en-us/azure/search/search-howto-indexing-azure-blob-storage">index for blob in Azure Search</a>, we will automatically detect these fields. If you already have Azure Search index created, you can add new fields (has to be the same as metadata key), and all changes will be synchronized with next re-indexing.</p>
