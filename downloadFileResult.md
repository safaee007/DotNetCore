# Download file result

### web api download file for client 

public async Task<FileResult> download()
{
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
    return null;
}


### dependency
namespace: System.IO.Compression.ZipFile

public static void CompressZipFolder(string startPath, string zipPath)
{
    ZipFile.CreateFromDirectory(startPath, zipPath);
}


