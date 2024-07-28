# easydemoadf

Azure resource creations:
1. Create a Resource Group.
2. Create Azure Key Vault with permission model as "Vault access policy".
3. Create Storage account with Gen2 for hierarchical namespace enabled and keep replication as locally redundant as it is only for demo.  
4. Create Azure Data Factory by ticking the git configuration for later.

Setting up Azure Key Vault:

1. Add secret for API key where source file will be accessible.
		Variable name - apikey
2. Add secret for snowflake to access snowflake from azure:
		Variable name - snowflakepass
3. Add secret management (Get and List) from key vault's access policies for azure data factory to access the secrets for API and snowflake.

Setting up Storage account:

 Create 3 containers such as raw, archive and logs.

Setting up repository:

Setup repository once ADF is launched.
Click setup repository and provide the GitHub account name as "saran0812", public access is granted so there won’t be any access issues.
Select easydemoadf as repository name from the drop down.
Select main the branch in the import option.
All required pipelines and datasets will be imported once repository setup is done.

Once pipelines and datasets are visible then linked services need to be refreshed and test the connection before triggering the pipeline.
Azure Key vault, storage account and snowflake connections need to be refreshed for your settings and check the connection.
Now go to cricketDailyDataLoad pipeline and go to getapi web activity to change the URL with the latest value from key vault secret.
Also change the azure blob storage account URLs in the select FileType execution activity (update the results and schedule scripts inside that activity)
Once connections are tested, validate all and publish the changes.
Repo link: https://github.com/saran0812/easydemoadf 

Setting up Snowflake:

Follow the script given for snowflake for warehouse, database, schema and tables creations.
Also, storage integration needs to be created under the name "easygo_api".
Take the given storage integration script and replace the azure tenant id as per your azure account settings.
Once integration is done, then describe the same to accept the permission to integrate with azure.
In Azure storage account ensure the snowflake service principle has storage blob data reader and storage blob data contributor access setup.

Repo link: https://github.com/saran0812/easysnowflake/tree/main 

Now trigger the pipeline called "masterpipeline".
If it doesn’t work, go to git configuration and click overwrite live mode and recheck the above "Setting up repository" steps again and trigger Master pipeline.
