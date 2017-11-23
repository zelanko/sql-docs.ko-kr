---
title: "외부 데이터 (분석 플랫폼 시스템) PolyBase 연결 구성"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6f14ac21-a086-4c05-861f-0a12bf278259
caps.latest.revision: "43"
ms.openlocfilehash: 7d486992f688b5bc914508ef000f23209b4bde89
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-polybase-connectivity-to-external-data"></a>외부 데이터 연결 PolyBase 구성
Hadoop 또는 Microsoft Azure 저장소 blob 데이터에 외부 원본에 연결 하려면 SQL Server PDW에서 PolyBase를 구성 하는 방법에 설명 합니다. PolyBase를 사용 하 여 Hadoop, Azure blob 저장소, SQL Server PDW를 비롯 한 여러 원본의 데이터를 통합 하는 쿼리를 실행 합니다.  
  
### <a name="to-configure-connectivity"></a>연결을 구성 하려면  
  
1.  Sqlcmd 또는 SQL Server 데이터 도구 (SSDT), 같은 쿼리 도구를 열고 sp_configure 'hadoop c 현재 설정을 보려면를 실행 합니다.  
  
    ![hadoop 연결 설정](./media/configure-polybase-connectivity-to-external-data/APS_PDW_sp_configure.png "APS_PDW_sp_configure")  
  
2.  Hadoop 연결 설정 필요 하 고 현재 설정을 변경 해야 하는지 여부를 결정 합니다. 이 옵션은 SQL Server PDW 영역 전체에 적용합니다. 구성 설정 및 버전의 전체 목록을 참조 하십시오. [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)합니다.  
  
3.  'Hadoop c 설정을 변경 하려면 sp_configure RECONFIGURE를 실행 합니다. 다음은 몇 가지 예입니다.  
  
    ```sql  
    --Enable connectivity to Hortonworks Data Platform for Windows Server (HDP), HDInsight on Analytics Platform System, or HDInsight’s Microsoft Azure blob storage  
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
  
    RECONFIGURE 함께 sp_configure를 실행 중인 구성 값을 설정합니다. 실행된 값을 설정 하는 영역을 다시 시작 필요 합니다. 이므로 컴퓨터를 다시 시작 필요 다음 중지 후도,에 코어 site.xml 변경 하는 다음 단계 이후까지 다시 시작을 수행할 필요가 없습니다.  
  
4.  외부 데이터 원본으로 Microsoft Azure blob 저장소를 사용 하려면 PDW 코어 site.xml 파일에 하나 이상의 Microsoft Azure 저장소 계정 액세스 키를 추가 합니다. 키를 추가 합니다.  
  
    1.  Microsoft Azure 저장소 계정 이름을 찾습니다. 저장소 계정, 로그인을 보려면는[Azure 포털](https://portal.azure.com) 클릭 **저장소 계정 (클래식)**합니다.  
  
        ![Windows Azure 저장소 계정 이름](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountName.png "APS_PDW_AzureStorageAccountName")  
  
    2.  Azure 저장소 계정 액세스 키를 찾습니다. 이 수행 하려면 저장소 계정 이름을 클릭 하 고 설정 블레이드에서 클릭 **키**합니다. 이 계정 이름과 저장소 키를 표시 됩니다.  
  
        ![Windows Azure 저장소 계정 액세스 키](./media/configure-polybase-connectivity-to-external-data/APS_PDW_AzureStorageAccountAccessKey.png "APS_PDW_AzureStorageAccountAccessKey")  
  
    3.  PDW 제어 노드에 원격 데스크톱 연결을 엽니다.  
  
    4.  C:\Program Files\Microsoft SQL Server 병렬 데이터 Warehouse\100\Hadoop\conf\core-site.xml 파일을 엽니다.  
  
    5.  코어 site.xml을 특성 이름 및 값을 가진 다음 속성을 추가 합니다.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.<your storage account name>.blob.core.windows.net</name>  
          <value><your storage account access key></value>  
        </property>  
        ```  
  
        이 예제에서는 앞에 표시 된 계정 이름과 액세스 키를 사용 합니다.  
  
        ```xml  
        <property>  
          <name>fs.azure.account.key.CustomerX.blob.core.windows.net</name>  
          <value>yyeTfCxxxxxxxxQ5WdnapXw77W+FwzHUhX/p/f26fIpnNFGtewzyRN90e1/qmTOl1xxxxxxxxa0goG71LsNcw==</value>  
        </property>  
        ```  
  
        > [!CAUTION]  
        > 코어 site.xml의 선택 키를 저장 하기 전에 보안 예방 조치를 취해야 합니다. CONTROL SERVER 또는 ALTER ANY EXTERNAL DATA SOURCE 권한을 가진 사용자는이 계정에 액세스 하는 외부 데이터 원본을 만들 수 있습니다. 외부 데이터 원본을 만든 후 테이블을 만들 수 있는 권한을 가진 모든 SQL Server PDW 사용자가 저장소 계정에 액세스 하는 외부 테이블을 만들 수 있습니다. 사용자 계정 데이터에 액세스 하 고 계정에서 리소스를 사용 하려면 다음 수 수 있습니다.  
  
    6.  코어 site.xml의 변경 내용을 저장 합니다.  
  
5.  Yarn-site.xml 파일로 yarn.application.classpath 속성 및 값을 추가 합니다.  
  
    외부 Hadoop 1.3에 연결 하는 경우이 단계를 건너뜁니다.  
  
    Hadoop 2.0 이후부터 yarn-site.xml 파일은 Hadoop YARN 프레임 워크에 대 한 구성 설정을 포함 합니다. 이 파일이 컨트롤 노드 아래에 있는 **C:\program files\Microsoft SQL Server 병렬 데이터 Warehouse\100\Hadoop\conf\\**합니다.  
  
    PolyBase 쿼리는 외부 Hadoop 2.0 클러스터에 대해 Windows 또는 Linux를 실행 하려면 yarn.application.classpath 속성 및 외부 Hadoop 클러스터에 yarn-site.xml 설정을 사용 하 여 일치 하는 값을 구성 해야 합니다. 이 구성은 외부 Hadoop 클러스터에는 기본 설정을 사용 하는 경우에 필요 합니다.  
  
    기본 설정 예:  
  
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
  
    재산 yarn-site.xml에서 정의 되 면 PolyBase는 HDInsight 지역에 대 한 쿼리를 실행 하는 경우 이러한 속성 설정을 사용 합니다. HDInsight 지역 및 외부 Hadoop 2.0 클러스터 모두에 대해 Windows에서 PolyBase 쿼리를 실행 하려는 경우 모든 yarn-site.xml 파일 간에 일관성 이어야 합니다. 그렇지 않으면 PolyBase 쿼리가 실패 합니다.  
  
    PolyBase HDInsight 지역 및 외부 Hadoop 2.0 클러스터 모두에 대해를 실행 하려면 외부 Hadoop 클러스터에 yarn-site.xml 기본 설정을 사용 합니다.  
  
6.  PDW 영역 다시 시작 합니다. 이 작업을 수행 하려면 구성 관리자 도구를 사용 합니다. 참조 [구성 관리자 &#40; 시작 분석 플랫폼 시스템 &#41; ](launch-the-configuration-manager.md).  
  
7.  Hadoop 연결에 대 한 보안 설정을 확인 합니다. 경우는 **약한 인증** Hadoop에서 쪽을 사용 하 여 사용 하도록 설정 `dfs.permission = true`, Hadoop 사용자를 만들어야 합니다 **pdw_user** 전체 읽기 권한을 부여 하 고이 사용자에 게 쓰기 권한이 있습니다. SQL Server PDW 및 SQL Server PDW에서 해당 호출은 항상으로 발급 **pdw_user** 는 고정 된 사용자 이름 인지 그리고이 Hadoop 연결 및 SQL Server PDW 릴리스이 버전을 변경할 수 없습니다. 사용 하 여 Hadoop에서 보안을 해제 하는 경우 `dfs.permission = false`, 더 이상 매크로 수행 해야 합니다.  
  
8.  Microsoft Azure blob 저장소에 외부 데이터 원본을 만들 수 있는 사용자를 결정 합니다. 저장소 계정 이름을 해당 사용자 지정 및 **ALTER ANY EXTERNAL DATA SOURCE** 또는 **제어 서버** 권한.  
  
9. Hadoop 연결에 대 한 Hadoop에 외부 데이터 원본을 만들 수 있는 사용자를 결정 합니다. 이러한 사용자의 각 노드의 각 Hadoop 이름, IP 주소와 포트 번호를 지정 하 고 제공 **ALTER ANY EXTERNAL DATA SOURCE** 또는 **제어 서버** 권한.  
  
10. WASB에 연결 하려면 DNS 전달 기기에서 구성할도 필요 합니다. DNS 전달 구성 하려면 참조 [해결 비 어플라이언스 DNS 이름 &#40; DNS 전달자를 사용 하 여 분석 플랫폼 시스템 &#41; ](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md).  
  
이제 권한이 있는 사용자가 외부 데이터 원본, 외부 파일 형식을 외부 테이블을 만들 수 있습니다. 사용 하 여 이러한 Hadoop, 포함 하 여 여러 원본의 데이터를에서 통합할 Microsoft Azure blob 저장소 및 SQL Server PDW 합니다.  
  
## <a name="see-also"></a>관련 항목:  
[어플라이언스 구성 &#40; 분석 플랫폼 시스템 &#41;](appliance-configuration.md)  
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
