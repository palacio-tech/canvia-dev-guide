Artworks
==================

Fields
------------------------


.. list-table::
    :header-rows: 1

    * - Field
      - Type
      - Description
    * - _id
      - Schema.Types.ObjectId
      - Id of the artwork in database
    * - title
      - String
      - Title for the painting
    * - details
      - String
      - More detailed description about the painting
    * - artist
      - String
      - The person who created the painting
    * - artist_ref
      - Schema.Types.ObjectId
      - Reference to the artist document
    * - copyright
      - String
      - Details of who holds the copyright for the artwork
    * - medium
      - String
      - The medium used for the painting
    * - classification
      - String
      - Classification of the painting in museum database
    * - accession
      - String
      - Accession number assigned to the painting in museum database
    * - date
      - String
      - Date when the painting was created (typically just year)
    * - dimensions
      - String
      - Physical dimensions of the original painting
    * - url_hash
      - String
      - No Idea
    * - credit
      - String
      - Credit line for the painting
    * - imageid
      - String
      - The GUID used to store the image in S3
    * - md5
      - String
      - The md5 hash for the image in artwork
    * - s3_bucket
      - String
      - The bucket name in S3 in which the original image is stored
    * - s3_key
      - String
      - The in the S3 bucket with which the original image is stored
    * - image_file_path
      - String
      - The location where the painting is stored in S3 (key + bucket)
    * - href
      - String
      - The URL from which the painting was acquired
    * - download_link
      - String
      - No Idea
    * - thumbnail
      - String
      - ? URL to the thumbnail of the painting
    * - thumbnail_s3_bucket
      - String
      - The S3 bucket in which the thumbnail is stored
    * - thumbnail_s3_key
      - String
      - Key of thumbnail in S3 bucket
    * - page_url
      - String
      - The URL of the page from where the image was sourced
    * - tags
      - [String]
      - Tags associated with the painting
    * - orientation
      - String
      - Default orientation of the picture for the painting
    * - art_forms
      - [String]
      - (DEP) Art forms associated with this painting
    * - art_types
      - [String]
      - (DEP) Art types associated with this painting
    * - painting_styles
      - [String]
      - (DEP) Painting styles associated with this painting
    * - eras
      - [String]
      - Eras to which the painting belongs
    * - subjects
      - [String]
      - Subjects to which the painting belongs
    * - movements
      - [String]
      - Movements to which the painting belongs
    * - mediums
      - [String]
      - Mediums to which the painting belongs
    * - colors
      - [String]
      - Predominant colors in the artwork
    * - source
      - String
      - Source from which palacio obtained the painting
    * - paid
      - Boolean
      - Indicates if the artwork is paid or not
    * - image_info
      - Object 
      - Original image (width, height, channels, size)
    * - public
      - Boolean
      - Public vs private artwork
    * - userId
      - String
      - User to which the artwork belongs.
    * - publication_status
      - String
      - Publication status of the artwork
    * - pub_wf_log
      - [TransitionLogEntry]
      - Log for publication workflow
    * - programs
      - Object
      - Monetization programs (premium, one-time)
