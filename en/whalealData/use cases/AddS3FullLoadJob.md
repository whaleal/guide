#### Adding an S3 Full Load Job

To add a new S3 full load job to the platform, follow these steps:

1. Click on the "Configuration Management" menu and select "Table Job Configuration".
2. In the S3 Table Job page, click the blue "Add" button to open the form.
3. Choose the data source database table and the target S3 bucket you want to synchronize. Ensure that the source endpoint is MongoDB's Gridfs data as the source for S3 synchronization.
4. Select "Full Load" as the archive mode.
5. The table job also includes data consistency verification. If you choose to enable it, you can set the required verification percentage. After the synchronization, the platform will perform data consistency checks on the synchronized data.
6. Since S3 has the characteristic that files with the same name will overwrite the existing files, you can choose from synchronization modes like "Replace without Handling", "Replace with Newest Files", or "ID + Filename" mode.
7. Choose a data processing method, either manual deletion or automatic deletion, after synchronization. The data source table will be deleted according to your choice after synchronization is completed.

![Adding an S3 Full Load Job](../../../images/whalealDataImages/image-20230621135150997.png)

By following these steps, you can create an S3 full load job that synchronizes data from a MongoDB Gridfs data source to a target S3 bucket. This allows for efficient management and synchronization of data between different storage systems within the Whaleal Data platform.