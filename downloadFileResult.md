# Download file result

### web api download file for client 

    var mimeType = 'application/x-zip-compressed';
    try
    {
        //make zip file OR exist zip file
        string sourceDirectory = "sourceDirectory path";
    
        IFileProvider provider = new PhysicalFileProvider(sourceDirectory);
        IFileInfo fileInfo = provider.GetFileInfo(filename.ToString() + ".zip");
        var readStream = fileInfo.CreateReadStream();
        return File(readStream, mimeType, filename.ToString());
    }
    catch (Exception)
    {

    }




### dependency
namespace System.IO.Compression.ZipFile

ZipFile.CreateFromDirectory(startPath, zipPath);



