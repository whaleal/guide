# Summary
* [Whaleal](README.md)
  * [Whaleal Platform](whalelaPlatform/README.md)
      * Overview
          * [Introduction](whalelaPlatform/00-Overview/01-Introduction.md)
          * [Comparison](whalelaPlatform/00-Overview/02-Comparison.md)
          
      * Install
          * [Requirement](whalelaPlatform/01-Intstall/00-requirement.md)
          * [Installation](whalelaPlatform/01-Intstall/01-Installation.md)
          
      * Usage
      
          * [Project](whalelaPlatform/02-Usage/Project.md)
      
          * Account
              * [AccountCenter](whalelaPlatform/02-Usage/Account/AccountCenter.md)
              * [Config](whalelaPlatform/02-Usage/Account/Config.md)
              * [Users](whalelaPlatform/02-Usage/Account/Users.md)
          * Server
              * [EC2](whalelaPlatform/02-Usage/Server/EC2.md)
              * [K8S](whalelaPlatform/02-Usage/Server/K8S.md)
              * [HostInfos](whalelaPlatform/02-Usage/Server/HostInfos.md)
              * [RemoveHost](whalelaPlatform/02-Usage/Server/RemoveHost.md)
          * MongoDB
              * CreateDeployment
                  * [CreateReplicaSet](whalelaPlatform/02-Usage/MongoDB/CreateDeployment/CreateReplicaSet.md)
                  * [CreateShardedCluster](whalelaPlatform/02-Usage/MongoDB/CreateDeployment/CreateShardedCluster.md)
                  * [CreateStandalone](whalelaPlatform/02-Usage/MongoDB/CreateDeployment/CreateStandalone.md)
                  * [ExistingMongoDBDeployment](whalelaPlatform/02-Usage/MongoDB/CreateDeployment/ExistingMongoDBDeployment.md)
              * ManageCluster
                  * clusteroperations
                    * [Connecttothecluster](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Connecttothecluster.md)
                    * [Updateclusterinformation](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Updateclusterinformation.md)
                    * [Clusterstartupshutdown](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Clusterstartupshutdown.md)
                    * [outofmanagement](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/outofmanagement.md)
                    * [Clusterrename](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Clusterrename.md)
                    * [Versionchanges](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Versionchanges.md)
                    * [Clusterchanges](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Clusterchanges.md)
                    * [clusterconversion](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/clusterconversion.md)
                    * [Turnonmonitoring](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Turnonmonitoring.md)
                    * [Enablelogcollection](whalelaPlatform/02-Usage/MongoDB/ManageCluster/clusteroperations/Enablelogcollection.md)
                  * [UserManagement](whalelaPlatform/02-Usage/MongoDB/ManageCluster/UserManagement.md)
                  * [Certification](whalelaPlatform/02-Usage/MongoDB/ManageCluster/Certification.md)
                  * [MonitorMongoDB](whalelaPlatform/02-Usage/MongoDB/ManageCluster/MonitorMongoDB.md)
              * [ManageCluster](whalelaPlatform/02-Usage/MongoDB/ManageCluster.md)
          * [Backuprestore]()
              * [Backub](whalelaPlatform/02-Usage/Backuprestore/Backub.md)
              * [Restore](whalelaPlatform/02-Usage/Backuprestore/Restore.md)
          * [Alert](whalelaPlatform/02-Usage/Alert.md)
          * [Diagnose]()
              * [Info](whalelaPlatform/02-Usage/Diagnose/Info.md)
              * [Health](whalelaPlatform/02-Usage/Diagnose/Health.md)
              * [Performance](whalelaPlatform/02-Usage/Diagnose/Performance.md)
              * [LogVis](whalelaPlatform/02-Usage/Diagnose/LogVis.md)
              * [ExplainPlan](whalelaPlatform/02-Usage/Diagnose/ExplainPlan.md)
          * [Message](whalelaPlatform/02-Usage/Message.md)
          * [Audit](whalelaPlatform/02-Usage/Audit.md)
          * [Settings]()
              * [UploadMongoDBTARfile](whalelaPlatform/02-Usage/Settings/UploadMongoDBTARfile.md)
              * [Emailconfiguration](whalelaPlatform/02-Usage/Settings/Emailconfiguration.md)
              * [Collectiongranularityconfiguration](whalelaPlatform/02-Usage/Settings/Collectiongranularityconfiguration.md)
              * [Kubernetesconfiguration](whalelaPlatform/02-Usage/Settings/Kubernetesconfiguration.md)
              * [InspectingS3configuration](whalelaPlatform/02-Usage/Settings/InspectingS3configuration.md)
          * [Support]()
              * [patrolinspection](whalelaPlatform/02-Usage/Support/patrolinspection.md)
      
      * UseCases
          * [HowToCreateReplicaSet](whalelaPlatform/03-UseCases/HowToCreateReplicaSet.md)
          * [HowToCreateShardedCluster](whalelaPlatform/03-UseCases/HowToCreateShardedCluster.md)
          * [HowToCreateStandalone](whalelaPlatform/03-UseCases/HowToCreateStandalone.md)
          * [HowToFindBottleNeckinHost](whalelaPlatform/03-UseCases/HowToFindBottleNeckinHost.md)
          * [HowToFindBottleNeckinMongoDB](whalelaPlatform/03-UseCases/HowToFindBottleNeckinMongoDB.md)
          
      * TroubleShooting
          * [AddHostFailed](whalelaPlatform/04-Troubleshooting/AddHostFaild.md)
          * [LoginFailed](whalelaPlatform/04-Troubleshooting/LoginFaild.md)
          * [MongoFailed](whalelaPlatform/04-Troubleshooting/MongoFaild.md)
          
      * ReleaseNotes
          * [ReleaseNote-1.0.0](whalelaPlatform/05-ReleaseNotes/releaseNote-1.0.0.md)
          
      * FAQ
          * [ForOpsManagerUser](whalelaPlatform/06-FAQ/ForOpsManagerUser.md)
          * [ForPMMUser](whalelaPlatform/06-FAQ/ForPMMUser.md)
          * [ForZabbixUser](whalelaPlatform/06-FAQ/ForZabbixUser.md)
          * [QA](whalelaPlatform/06-FAQ/QA.md)
          
      * APIReference
          * [Agent](whalelaPlatform/07-APIReference/Agent.md)
          * [Alert](whalelaPlatform/07-APIReference/Alert.md)
          * [Collection](whalelaPlatform/07-APIReference/Collection.md)
          * [DBData](whalelaPlatform/07-APIReference/MongoDbData.md)
          * [ErrorCodes](whalelaPlatform/07-APIReference/ErrorCodes.md)
          * [Files](whalelaPlatform/07-APIReference/Files.md)
          * [Member](whalelaPlatform/07-APIReference/Member.md)
          * [Mongo](whalelaPlatform/07-APIReference/MongoOperate.md)
          * [Other](whalelaPlatform/07-APIReference/Other.md)
          * [Third_party](whalelaPlatform/07-APIReference/Third_party.md)
          * [Configuration](whalelaPlatform/07-APIReference/Configuration.md)
          * [Analysis](whalelaPlatform/07-APIReference/Analysis.md)
          * [Project](whalelaPlatform/07-APIReference/Project.md)
      
  * [Whaleal Data](whalealData/README.md)
      
      * InstallationDeployment
          * [InstallationRequirements](whalealData/InstallationDeployment/InstallationRequirements.md)
          * [JDKInstallationDeployment](whalealData/InstallationDeployment/JDKInstallationDeployment.md)
          * [MYSQLInstallationDeployment](whalealData/InstallationDeployment/MYSQLInstallationDeployment.md)
          * [NginxInstallationDeployment](whalealData/InstallationDeployment/NginxInstallationDeployment.md)
          * [RedisInstallationDeployment](whalealData/InstallationDeployment/RedisInstallationDeployment.md)
          * [ZookeeperInstallationDeployment](whalealData/InstallationDeployment/ZookeeperInstallationDeployment.md)
          * [Whaleal-dataInstallationDeployment](whalealData/InstallationDeployment/Whaleal-dataInstallationDeployment.md)
      * Whaleal data Manual
          * LoginPage
              * [UserFirstLogin](whalealData/UserManual/LoginPage/UserFirstLogin.md)
              * [UserRegistration](whalealData/UserManual/LoginPage/UserRegistration.md)
          * [HomepageDisplay](whalealData/UserManual/HomepageDisplay/HomepageDisplay.md)
          * ConfigurationManagement
              * [DataSourceManagement](whalealData/UserManual/ConfigurationManagement/DataSourceManagement.md)
              * [DestinationSourceManagement](whalealData/UserManual/ConfigurationManagement/DestinationSourceManagement.md)
              * [TableJobConfiguration](whalealData/UserManual/ConfigurationManagement/TableJobConfiguration.md)
              * [TaskConfiguration](whalealData/UserManual/ConfigurationManagement/TaskConfiguration.md)
          * TaskManagement
              * [TaskScheduling](whalealData/UserManual/TaskManagement/TaskScheduling.md)
              * [WarmTaskMonitoring](whalealData/UserManual/TaskManagement/WarmTaskMonitoring.md)
              * [ColdTaskMonitoring](whalealData/UserManual/TaskManagement/ColdTaskMonitoring.md)
              * [S3TaskMonitoring](whalealData/UserManual/TaskManagement/S3TaskMonitoring.md)
          * ArchiveManagement
              * [ColdTaskLogQuery](whalealData/UserManual/ArchiveManagement/ColdTaskLogQuery.md)
              * [FileInspectionManagement](whalealData/UserManual/ArchiveManagement/FileInspectionManagement.md)
              * [FileFullTextSearch](whalealData/UserManual/ArchiveManagement/FileFullTextSearch.md)
          * SystemManagement
              * [UserManagement](whalealData/UserManual/SystemManagement/UserManagement.md)
              * [RoleManagement](whalealData/UserManual/SystemManagement/RoleManagement.md)
              * [MenuManagement](whalealData/UserManual/SystemManagement/MenuManagement.md)
              * [SystemSettings](whalealData/UserManual/SystemManagement/SystemSettings.md)
              * [OperationLog](whalealData/UserManual/SystemManagement/OperationLog.md)
              * [ErrorLog](whalealData/UserManual/SystemManagement/ErrorLog.md)
          * StatisticalReports
              * [TableJobExecutionStatistics](whalealData/UserManual/StatisticalReports/TableJobExecutionStatistics.md)
              * [AbnormalJobExecutionStatistics](whalealData/UserManual/StatisticalReports/AbnormalJobExecutionStatistics.md)
              * [SystemAccessStatistics](whalealData/UserManual/StatisticalReports/SystemAccessStatistics.md)
              * [RollbackRecordsStatistics](whalealData/UserManual/StatisticalReports/RollbackRecordsStatistics.md)
              * [JobDetails](whalealData/UserManual/StatisticalReports/JobDetails.md)
              * [DataHistoricalFlow](whalealData/UserManual/StatisticalReports/DataHistoricalFlow.md)
      * use Cases
          * [UserRegistration](whalealData/use cases/UserRegistration.md)
          * [UserLogin](whalealData/use cases/UserLogin.md)
          * [AddDataSource](whalealData/use cases/AddDataSource.md)
          * [AddDestinationSource](whalealData/use cases/AddDestinationSource.md)
          * [AddWarmDataFullLoadJob](whalealData/use cases/AddWarmDataFullLoadJob.md)
          * [AddColdDataFullLoadJob](whalealData/use cases/AddColdDataFullLoadJob.md)
          * [AddS3FullLoadJob](whalealData/use cases/AddS3FullLoadJob.md)
          * [AddWarmDataIncrementalJob](whalealData/use cases/AddWarmDataIncrementalJob.md)
          * [AddColdDataIncrementalJob](whalealData/use cases/AddColdDataIncrementalJob.md)
          * [AddS3IncrementalJob](whalealData/use cases/AddS3IncrementalJob.md)
          * [CreateSingleTask](whalealData/use cases/CreateSingleTask.md)
          * [CreateManualTask](whalealData/use cases/CreateManualTask.md)
          * [CreateLoopTask](whalealData/use cases/CreateLoopTask.md)
          * [TaskExecutionMonitoring](whalealData/use cases/TaskExecutionMonitoring.md)
          * [RetryAbnormalTask](whalealData/use cases/RetryAbnormalTask.md)
          * [AbnormalTaskFeedback](whalealData/use cases/AbnormalTaskFeedback.md)
          * [SystemDeleteSourceData](whalealData/use cases/SystemDeleteSourceData.md)
          * [ManuallyDeleteSourceData](whalealData/use cases/ManuallyDeleteSourceData.md)
          * [ColdDataWriteBack](whalealData/use cases/ColdDataWriteBack.md)
          * [ColdDataFullTextSearch](whalealData/use cases/ColdDataFullTextSearch.md)
          * [SMTPConfig](whalealData/use cases/SMTPConfig.md)
          * [WarmJobDemo](whalealData/use cases/WarmJobDemo.md)
          * [ColdWorkDemo](whalealData/use cases/ColdWorkDemo.md)
          * [S3JobDemo](whalealData/use cases/S3JobDemo.md)
      
  * [Document Data Transfer](documentDataTransfer/README.md)
      * Overview
        * [Architecture](documentDataTransfer/Introduction/Architecture.md)
        * [CustomerCase](documentDataTransfer/Introduction/CustomerCase.md)
      * Install
        * [Requirements](documentDataTransfer/Install/Requirements.md)
        * [Installation](documentDataTransfer/Install/Installation.md)
        * [QuickStart](documentDataTransfer/Install/QuickStart.md)
        * [Configuring](documentDataTransfer/Install/Configuring.md)
      * Use Case
        * [FunctionalTest](documentDataTransfer/Usecase/FunctionalTest.md)
        * [FullTesting](documentDataTransfer/Usecase/FullTesting.md)
        * [RealTimeTest](documentDataTransfer/Usecase/RealTimeTest.md)
      
  * [Whaleal Account](whalealAccount/README.md)
      * Oauth2 
        * [Oauth2](whalealAccount/Oauth2/oauth2.md)
      * UserManual
        * [Register](whalealAccount/UserManual/register.md)
        * [Login](whalealAccount/UserManual/login.md)
        * [PasswordReset](whalealAccount/UserManual/passwordReset.md)
        * [UserInfo](whalealAccount/UserManual/userInfo.md)
        * [Organization](whalealAccount/UserManual/organization.md)
        * [Client](whalealAccount/UserManual/client.md)
      
  * [Whaleal Support](whalealSupport/README.md)
      * UserManual
        * [Login](whalealSupport/UserManual/login.md)
        * [Create Case According To SLA](whalealSupport/UserManual/createCaseAccordingToSLA.md)
        * [MyCaseList](whalealSupport/UserManual/myCaseList.md)
        * [CaseDetails](whalealSupport/UserManual/caseDetails.md)
        * [ProductionAndDocument](whalealSupport/UserManual/productionAndDocument.md)
        * [Notification](whalealSupport/UserManual/notification.md)
        * [AddressList](whalealSupport/UserManual/addressList.md)
