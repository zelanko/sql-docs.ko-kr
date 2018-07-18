---
title: Analytics Platform System-PolyBase 연결 구성 | Microsoft Docs
description: 외부 Hadoop 또는 Microsoft Azure storage blob 데이터 원본에 연결할 Parallel Data Warehouse에서 PolyBase를 구성 하는 방법을 설명 합니다. PolyBase를 사용 하 여 Hadoop, Azure blob storage 및 병렬 데이터 웨어하우스를 포함 하 여 여러 원본에서 데이터를 통합 하는 쿼리를 실행 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 26eeffb1d2a27ee49f01114b015ab4051b145d64
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909873"
---
# <a name="configure-polybase-connectivity-to-external-data"></a>외부 데이터에 대 한 PolyBase 연결 구성
외부 Hadoop 또는 Microsoft Azure storage blob 데이터 원본에 연결할 Parallel Data Warehouse에서 PolyBase를 구성 하는 방법을 설명 합니다. PolyBase를 사용 하 여 Hadoop, Azure blob storage 및 병렬 데이터 웨어하우스를 포함 하 여 여러 원본에서 데이터를 통합 하는 쿼리를 실행 합니다.  
  
### <a name="to-configure-connectivity"></a>연결을 구성 하려면  
  
1.  Sqlcmd 또는 SQL Server 데이터 도구 (SSDT), 같은 쿼리 도구를 열고 sp_configure 'hadoop 연결' 현재 설정을 보려면를 실행 합니다.  
  
    ![hadoop 연결 설정](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Hadoop 연결 설정 및 현재 설정을 변경 해야 하는지 여부를 결정 합니다. 이 옵션은 전체 SQL Server PDW 영역에 적용 됩니다. 구성 설정 및 버전의 전체 목록을 참조 하세요 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)합니다.  
  
3.  'Hadoop 연결' 설정을 변경 하려면 RECONFIGURE를 사용 하 여 sp_configure를 실행 합니다. 몇 가지 예는 다음과 같습니다.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP) or HDInsight’s Microsoft Azure blob storage  
    EXEC sp_configure 'hadoop connectivity', 4;   
    RECONFIGURE;  
  
    -- Enable connectivity to Hortonworks Data Platform (HDP)for Linux   
    EXEC sp_configure 'hadoop connectivity', 5;   
    RECONFIGURE;  
  
    -- Enable connectivity to Cloudera CDH for Linux   
    EXEC sp_configure 'hadoop connectivity', 3;   
    RECONFIGURE;  
  
    -- Disable the Hadoop connectivity option   
    EXEC sp_configure 'hadoop connectivity', 0;  
    RECONFIGURE;  
    ```  
  
    RECONFIGURE 함께 sp_configure를 실행 중인 구성 값을 설정 합니다. 실행된 값을 설정 하는 영역을 다시 시작 필요 합니다. 이므로 다시 시작 필요 다음 중지 후 또한 core-site.xml 변경 하는 다음 단계를 수행한 후 될 때까지 다시 시작을 수행할 필요가 없습니다.  
  
4.  외부 데이터 원본으로 Microsoft Azure blob storage를 사용 하려면 하나 이상의 Microsoft Azure storage 계정 액세스 키를 PDW core-site.xml 파일에 추가 합니다. 키를 추가 합니다.  
  
    1.  Microsoft Azure 저장소 계정 이름을 찾습니다. 저장소 계정에 로그인을 보려면 합니다[Azure portal](https://portal.azure.com) 클릭 **저장소 계정 (클래식)** 합니다.  
  
        ![Windows Azure 저장소 계정 이름](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Azure storage 계정 액세스 키를 찾습니다. 이렇게 하려면 저장소 계정 이름을 클릭 하 고 설정 블레이드에서 클릭 **키**합니다. 계정 이름 및 저장소 키 표시 합니다.  
  
        ![Windows Azure 저장소 계정 액세스 키](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  PDW 제어 노드에 원격 데스크톱 연결을 엽니다.  
  
    4.  C:\Program Files\Microsoft SQL Server 병렬 데이터 Warehouse\100\Hadoop\conf\core-site.xml 파일을 엽니다.  
  
    5.  특성 이름 및 값을 사용 하 여 다음 속성을 core-site.xml에 추가 합니다.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        이 예제에서는 이전에 표시 된 계정 이름과 액세스 키를 사용 합니다.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > Core-site.xml에 대 한 액세스 키를 저장 하기 전에 보안 예방 조치를 수행 합니다. CONTROL SERVER 또는 ALTER ANY EXTERNAL DATA SOURCE 권한이 있는 모든 사용자는이 계정에 액세스 하는 외부 데이터 원본을 만들 수 있습니다. 외부 데이터 원본이 만들어지면 CREATE TABLE 권한 가진 모든 SQL Server PDW 사용자는이 저장소 계정에 액세스 하는 외부 테이블을 만들면 됩니다. 사용자 계정 데이터에 액세스 하는 계정에서 리소스를 사용 여 합니다.  
  
    6.  Core-site.xml에 저장 합니다.  
  
5.  Yarn-site.xml 파일로 yarn.application.classpath 속성 및 값을 추가 합니다.  
  
    외부 Hadoop 1.3에 연결 하는 경우이 단계를 건너뜁니다.  
  
    Hadoop 2.0 부터는 yarn-site.xml 파일은 Hadoop YARN 프레임 워크에 대 한 구성 설정을 포함 합니다. 이 파일이 컨트롤 아래에 있는 **C:\program files\Microsoft SQL Server 병렬 데이터 Warehouse\100\Hadoop\conf\\**합니다.  
  
    PolyBase 쿼리는 외부 Hadoop 2.0 클러스터에 대해 Windows 또는 Linux를 실행 하려면 yarn.application.classpath 속성 및 외부 Hadoop 클러스터의 yarn-site.xml 설정과 일치 하도록 값을 구성 해야 합니다. 이 구성은 외부 Hadoop 클러스터에서 기본 설정을 사용 하는 경우에 필요 합니다.  
  
    기본 설정 예제:  
  
    ```xml  
    <property>  
        <name>yarn.application.classpath</name>  
        <value>  
          %HADOOP_CONF_DIR%,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/*,  
          %HADOOP_COMMON_HOME%/share/hadoop/common/lib/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/*,  
          %HADOOP_HDFS_HOME%/share/hadoop/hdfs/lib/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/*,  
          %HADOOP_YARN_HOME%/share/hadoop/yarn/lib/*  
         </value>  
      </property>  
    ```  
  
    속성 yarn-site.xml에서 정의 되 면 PolyBase Hadoop에 대해 쿼리를 실행할 때 이러한 속성 설정을 사용 합니다. Windows에서 Azure Storage Blob 및 외부 Hadoop 2.0 클러스터 둘 다에 대해 PolyBase 쿼리를 실행 하려는 경우 모든 yarn-site.xml 파일 일관성 이어야 합니다. 그러지 PolyBase 쿼리가 실패 합니다.  
   
6.  PDW 영역을 다시 시작 합니다. 이 작업을 수행 하려면 Configuration Manager 도구를 사용 합니다. 참조 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.  
  
7.  Hadoop 연결에 대 한 보안 설정을 확인 합니다. 경우는 **대 한 인증이 약하면** hadoop 쪽을 사용 하 여 사용 하도록 설정 `dfs.permission = true`, Hadoop 사용자를 만들어야 **pdw_user** 전체 읽기 권한을 부여 하 고이 사용자에 게 쓰기 권한을 합니다. SQL Server PDW 및 SQL Server PDW에서 해당 호출으로 항상 실행 됩니다 **pdw_user**합니다.  이 고정 된 사용자 이름 및이 Hadoop 연결 및 SQL Server PDW 릴리스이 버전을 변경할 수 없습니다. 보안 Hadoop 사용 하 여 비활성화 된 경우 `dfs.permission = false`에 없는 추가 작업을 수행 해야 합니다.  
  
8.  Microsoft Azure blob storage에 외부 데이터 원본을 만들 수 있는 사용자를 결정 합니다. 이러한 사용자 각각의 저장소 계정 이름을 제공 그리고 **ALTER ANY EXTERNAL DATA SOURCE** 하거나 **CONTROL SERVER** 권한.  
  
9. Hadoop 연결에 대 한 Hadoop에 외부 데이터 원본을 만들 수 있는 사용자를 결정 합니다. 이러한 사용자 각각의 각 Hadoop 이름 노드의 IP 주소와 포트 번호를 지정 하 고 부여할 **ALTER ANY EXTERNAL DATA SOURCE** 하거나 **CONTROL SERVER** 권한.  
  
10. WASB에 연결할 DNS 전달을 어플라이언스 구성도 필요 합니다. DNS 전달을 구성 하려면 [비 어플라이언스 DNS 이름 확인에 DNS 전달자를 사용 하 여 &#40;Analytics Platform System&#41;](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)합니다.  
  
권한 있는 사용자는 외부 데이터 원본, 외부 파일 형식 및 외부 테이블에 이제 만들 수 있습니다. 이러한 Hadoop을 비롯 한 여러 원본의 데이터를에서 통합 하는 데 사용할 수 Microsoft Azure blob storage 및 SQL Server PDW 합니다.  

## <a name="kerberos-configuration"></a>Kerberos 구성  
Note PolyBase가 Kerberos 보안된 클러스터에 인증 하는 경우 hadoop.rpc.protection 설정을 인증으로 설정 해야 합니다. 이렇게 하면 암호화되지 않은 Hadoop 노드 간의 데이터 통신이 유지됩니다. 

 [MIT KDC 사용] Kerberos 보안 Hadoop 클러스터를 연결 하려면:
   
  
1.  제어 노드에 설치 경로에서 Hadoop 구성 디렉터리를 찾습니다.  
  
    ```  
    C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf
    ```  
  
2.  아래 표에 나와 있는 구성 키의 Hadoop 쪽 구성 값을 찾습니다. 구성 파일은 Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 찾을 수 있습니다.  
  
3.  제어 노드에서 해당 파일 내에서 value 속성에 구성 값을 복사 합니다.  
  
    |**#**|**구성 파일**|**구성 키**|**동작**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|KDC 호스트 이름을 지정합니다. 예를 들면 kerberos.your-realm.com과 같습니다.|  
    |2|core-site.xml|polybase.kerberos.realm|Kerberos 영역을 지정합니다. 예를 들면 YOUR REALM.COM과 같습니다.|  
    |3|core-site.xml|hadoop.security.authentication|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예를 들면 KERBEROS와 같습니다.<br></br>**보안 정보:** KERBEROS는 대문자로 작성해야 합니다. 소문자로 작성되면 실행되지 않을 수 있습니다.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.address|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예를 들면 10.193.26.174:10020과 같습니다.|  
    |7|yarn-site.xml yarn|yarn.resourcemanager.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: yarn/_HOST@YOUR-REALM.COM|  
  
4. 데이터베이스 범위 자격 증명 개체를 만들어 각 Hadoop 사용자에 대해 인증 정보를 지정합니다. [PolyBase T-SQL 개체](../relational-databases/polybase/polybase-t-sql-objects.md)를 참조하세요.  

5. PDW 영역을 다시 시작 합니다. 이 작업을 수행 하려면 Configuration Manager 도구를 사용 합니다. 참조 [구성 관리자 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)합니다.
 
## <a name="see-also"></a>관련 항목  
[어플라이언스 구성 &#40;Analytics Platform System&#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
