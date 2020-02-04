# Realm in dot net core


### model
sample model 

public class OBsCategory : RealmObject
{
    [System.ComponentModel.DefaultValue("")]
    [Required]
    [PrimaryKey]
    public string UID { get; set; }

    [Required]
    [System.ComponentModel.DefaultValue("")]
    public string Title { get; set; }

    [Backlink(nameof(Book.Category))]
    public IQueryable<Book> Book { get; }
}

string realmPath = Path.Combine(realmDir, DBName);
var config = new RealmConfiguration(realmPath);
//config.SchemaVersion = 1;
var realm = Realm.GetInstance(config);


OBsCategory cat = new OBsCategory()
{
    UID = GUID.UID.ToString(),
    Title = "test"
};
vol.Category.Add(cats);

realm.Write(() => realm.Add(cat, update: true));
