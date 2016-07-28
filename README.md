# FacadePatternSample
It is simple playground file written in Swift language to demonstrate Facade Design Pattern

Sample Code :-
```Swift
class Album{
    var title: String
    var artist:  String
    var CoverURL: String
    
    init(title:String, artist:String, CoverURL:String){
        self.title = title
        self.artist = artist
        self.CoverURL = CoverURL
    }
}

class PersistencyManager {
    var albums: [Album]
    init(){
        albums = [Album (title: "Romance", artist: "Arijit", CoverURL: "https:www.xyz.com/movie1.png"),
                  Album (title: "Sad", artist: "Sonu", CoverURL: "https:www.xyz.com/movie2.png")]
        
    }
    func getAlbums() -> [Album] {
        return albums
    }
    func addAlbum(album:Album, atIndex:Int) {
        albums .insert(album, atIndex: atIndex)
    }
    func deleteAlbumAtIndex(atIndex:Int) {
        albums .removeAtIndex(atIndex)
    }
}


class LibraryAPI {
    var persistencyManager: PersistencyManager
    var isOnline : Bool
    init(){
        persistencyManager = PersistencyManager()
        isOnline = false
    }
    func getAlbums() -> [Album] {
        return persistencyManager .getAlbums()
    }
    func addAlbum(album:Album, atIndex:Int)  {
        persistencyManager .addAlbum(album, atIndex: atIndex)
        if isOnline {
            // Code to Add on Server --> Post Request
        }
    }
    func deleteAlbumAtIndex(atIndex:Int){
        persistencyManager .deleteAlbumAtIndex(atIndex)
        if isOnline {
            // Code to Delete from Server --> Post Request
        }
    }
}

let facadeClient = LibraryAPI()
facadeClient.addAlbum(Album(title: "Melodious", artist: "Kumar Sanu", CoverURL: "https:www.xyz.com/movie3.png"), atIndex: 2)
var albumLists = facadeClient.getAlbums()
for album in albumLists{
    print("Title :- \(album.artist), Artist :- \(album.title), Cover Page :- \(album.CoverURL)")
}
```
