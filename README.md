- 👋 Hi, I’m @TimoAbaData
# MMPKgenerator
Generate mobile map packages for companies based on Abadata2.FieldOps.AppMap table.

### All Script Files

# ConnectTable.py
    - Connects to DataBase using pyodbc py library.
    - ConnectTable.connect() returns connection varible.
    - ConnectTable(*connectionVarible) closes connection to DataBase.

# SQL_query.py
    - Functions to execute queries from DataBase
    - SQl_query.CustomQuery(*query, *connection, *params)
        - returns tuple ("Column Names", "Result/Response")
    - SQl_query.query_(*StoredProcedure, *params(if any), *connection)
        - returns tuple ("Column Names", "Result/Response")

# JSON_compare.py
    - Functions to get JSON opration.
    - JSON_compare.jsonDiff(*Old_JSON, *New_JSON) 
        - returns JSON difference between two input JSONs
    - JSON_compare.read(*JSON_path)
        - Reads Json from a given path and returns it as Dict.
    - JSON_compare.write(*JSON_data, *Path)
        - writes the dict as JSON in given location

# TableProcessor.py
    - Functions to do Updates and Insertions based on Map Inputs for new Maps.
    - Need to declare Path for 2 files (# AppMapLayersJSONpath =  AppLayers.json, # CompCodesPath = CompanyId.json)
    - TableProcessor.PreProcessingInserts(*AppID)
        - update Tables [FieldOps].[AppMapLayer], [FieldOps].[AppMapLayerAttributes], [FieldOps].[AppMapCompany] according to data from AppLayers.json and CompanyId.json on AbaData2 Database.
    - TableProcessor.Update_urls(*Maps_url_dict)
        - Update the table [FieldOps].[AppMapHistory] with new updated map urls from dropbox and update the MapUrls in table.

# DropboxUpload.py 
    - Functions to operate on DropBox usind Dropbox APIs
    - DropboxUpload.BeginUpload(*access_token, *refresh_token, *map_names{dict})
        - Need to declare 3 varibles (# app_key = "", app_secret  = "", MMPKs_path = Your Path folder containing MMPK maps)
        - creates new folder for Company if dosen't exists, 
        - if Map already exits in company folder it is moved into rollback and new Map is updated.
        - Returns MapDict with URls of each map on dropbox with AppMapIds as keys.

# SenbdMail.py
    - Functions to Send Mail to user to notify updates using smtplib, email (to construct body of message) py libraries.
    - SenbdMail.send_email(*Reciver_mail (can be list of recivers), *message, *attachments(if exixts):path) 
        - Sends Mail to list of recivers.

# MMPKgenerator.py
    - Main fucntion to generate MMPK maps for the company specifications.
    - MMPKgenerator.main(*AppID)
        - Retrives infomation about CompanyIds, Layers, Attributes, BoundingBox and other information required to generate from the DataBase Tables.
        - Checks if all required layers are on the maps, and adds layers if required layers are not in the map from Specified Location with symbology.
        - Generates MMPKs for partiuclar AppId company.
        - Returns AppMapId and MapName

# Main.py
    - Main Function to 
        - Update/Insert layer&Attribute information, 
        - Generate MMPKs, 
        - Upload Maps to Dropbox
        - Update Maps Urls into DataBase.

# @AppLayer.json
    - Json contain all layer & corresponding attributes information.

# @CompanyID.json
    - JSON contains all company codes required for the layer.


