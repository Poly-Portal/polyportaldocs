# Database Tables

**These documents reflect the tables in the design stage and may not be up to date. Use as reference only.**

![Image](./tables.png)

## DBML

The following is a DBML description of the database, Create a diagram at https://dbdiagram.io/ to view it. 

```
// Display: https://dbdiagram.io/
// Docs: https://dbml.dbdiagram.io/docs/


Table File {
  id bigserial [pk]
  fileExtension text [not null] // Used to select the three.js loader
  fileName text [not null]
  ownerUserId text [not null]
  uploadedAt timestamp
}



Table Artwork {
  id bigserial [pk]
  title text [not null]
  description text [not null]
  ownerUserId text [not null]
  downloadCount integer [not null, default: 0]
  viewCount integer [not null, default: 0]
  createdAt timestamp [not null]
  metaTriangleCount integer
  metaQuadCount integer
  metaPolygonCount integer
  metaTotalTriangleCount integer
  metaVerticesCount integer
  metaMaterialsCount integer
}

Enum FileType {
  MODEL
  TEXTURE
  MATERIAL
  THUMBNAIL
  OTHER
}

Table ArtworkFiles {
  artworkId bigserial [ref: > Artwork.id]
  artworkFileId bigserial [ref: > File.id]
  artworkVersion integer [not null]
  fileType FileType [not null]
  indexes {
    (artworkId, artworkFileId) [pk]
  }
}

Table ArtworkTags {
  artworkId bigserial [ref: > Artwork.id, not null]
  tag text [not null]

  Indexes {
    (artworkId, tag) [unique]
  }
}

Table ArtworkFileUploadTokens {
  jti text [pk]
  fileId bigserial [ref: > File.id, not null]
  consumed boolean [not null, default: FALSE]
}
```
