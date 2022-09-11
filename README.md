## Zapisywanie zdjęcia

```
fun savePhotoToInternalStorage(fileName: String, bmp: Bitmap): Boolean {
  
  return try {
    context.openFileOutput("$filename.jpg, MODE_PRIVATE).use {
      if(!bmp.compress(Bitmap.CompressFormat.JPEG,95,it)) {
        throw IOException("Couldn't save bitmap.")
      }
    }
  true
  } catch (e: IOException) {
      e.printStackTrace()
      false
    }
}
```

## Wczytywanie zdjęcia

```
fun suspend loadPhotosFromInternalStorage(): List<InternalStoragePhoto> {
  
  return withContent(Dispatchers.IO {
    val files = filesDir.listFiles() 
    files?.filter {
      it.canRead && it.isFile && it.name.endsWith(".jpg"
    }?map {
      val bytes = it.readBytes()
      val bmp = BitmapFactory.decodeByteArray(bytes,0,bytes.size)
      InternalStoragePhoto(it.name, bmp)
    }?: listOf()
  }
}
```

## Usuwanie plików

```
fun deletePhotoFromInternalStorage(filename: String): Boolean {
  
  return try {
    deleteFile(fileName)
  } catch (e: Exception) {
    e.printStackTrace
    false
  }
}
```

## Zapisywanie zdjęcia po zrobieniu

```
val takePhoto = registerForActivityForResult(ActivityResultContracts.TakePicturePreview()) {
 
  if(savePhotoToInternalStorage(UUID.randomUUID().toString, it)) {
  //Toast
  } else {
  //Toast
  }
```
  
