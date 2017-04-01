---
title: "PolyBase 구성 | Microsoft Docs"
ms.custom: ""
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80ff73c1-2861-438b-a13f-309155f3d6e1
caps.latest.revision: 17
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 12
---
# PolyBase 구성
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  PolyBase를 구성하려면 다음 절차를 수행합니다.  
  
## <a name="external-data-source-configuration"></a>외부 데이터 원본 구성  
 SQL Server에서 외부 데이터 원본에 대한 연결을 확인해야 합니다. 연결 형식에 따라 필요한 쿼리 성능이 크게 달라집니다. 예를 들어 PolyBase 쿼리에서 10Gbit 이더넷 링크를 사용하는 경우 1Gbit 이더넷 링크보다 쿼리 응답 속도가 빨라집니다.  
  
 **sp_configure**를 사용하여 SQL Server가 사용 중인 Hadoop 버전 또는 Azure Blob 저장소에 연결하도록 구성해야 합니다. PolyBase는 HDP(Hortonworks Data Platform) 및 CDH(Cloudera Distributed Hadoop)의 두 가지 Hadoop 배포를 지원합니다.  지원되는 외부 데이터 원본의 전체 목록은 [PolyBase Connectivity Configuration&#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.  
  
### <a name="run-spconfigure"></a>sp_configure 실행  
  
1.  sp_configure ‘hadoop connectivity’를 실행하고 적절한 값을 설정합니다.  값을 찾으려면 [PolyBase Connectivity Configuration&#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)을 참조하세요.  
  
    ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  **services.msc**를 사용하여 SQL Server를 다시 시작해야 합니다. SQL Server를 다시 시작하면 다음 서비스도 다시 시작됩니다.  
  
    -   SQL Server PolyBase 데이터 이동 서비스  
  
    -   SQL Server PolyBase 엔진  
  
## <a name="pushdown-configuration"></a>푸시다운 구성  
 쿼리 성능을 향상시키려면 Hadoop 클러스터에 대한 푸시다운 계산을 사용하도록 설정합니다.  
  
1.  SQL Server 설치 경로에서 **yarn-site.xml** 파일을 찾습니다. 일반적인 경로는 다음과 같습니다.  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 동일한 파일을 찾습니다. 이 파일에서 구성 키 yarn.application.classpath의 값을 찾아서 복사합니다.  
  
3.  SQL Server 컴퓨터의 **yarn.site.xml 파일** 에서 **yarn.application.classpath** 속성을 찾은 다음 Hadoop 컴퓨터의 값을 value 요소에 붙여넣습니다.  
  
## <a name="kerberos-configuration"></a>Kerberos 구성  
 Kerberos로 보호되는 Hadoop 클러스터에 연결하려면 다음 단계를 수행합니다[MIT KDC 사용].  
  
1.  SQL Server의 설치 경로에서 Hadoop 구성 디렉터리를 찾습니다. 일반적인 경로는 다음과 같습니다.  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf  
    ```  
  
2.  아래 표에 나와 있는 구성 키의 Hadoop 쪽 구성 값을 찾습니다. 구성 파일은 Hadoop 컴퓨터의 Hadoop 구성 디렉터리에서 찾을 수 있습니다.  
  
3.  구성 값을 SQL Server 컴퓨터의 해당 파일 내 value 속성에 복사합니다.  
  
    |**#**|**구성 파일**|**구성 키**|**동작**|  
    |------------|----------------|---------------------|----------|   
    |1|core-site.xml|polybase.kerberos.kdchost|Kerberos 영역을 지정합니다. 예를 들면 YOUR REALM.COM과 같습니다.|  
    |2|core-site.xml|polybase.kerberos.realm|KDC 호스트 이름을 지정합니다. 예를 들면 kerberos.your-realm.com과 같습니다.|  
    |3|core-site.xml|hadoop.security.authentication|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예를 들면 KERBEROS와 같습니다.<br></br>**보안 정보:** KERBEROS는 대문자로 작성해야 합니다. 소문자로 작성되면 실행되지 않을 수 있습니다.|   
    |4|hdfs-site.xml|dfs.namenode.kerberos.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: hdfs/_HOST@YOUR-REALM.COM|  
    |5|mapred-site.xml|mapreduce.jobhistory.address|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: mapred/_HOST@YOUR-REALM.COM|  
    |6|mapred-site.xml|mapreduce.jobhistory.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예를 들면 10.193.26.174:10020과 같습니다.|  
    |7|yarn-site.xml yarn|yarn.resourcemanager.principal|Hadoop 쪽 구성을 찾아 SSQL Server 컴퓨터에 복사합니다. 예: yarn/_HOST@YOUR-REALM.COM|  
  
4.  데이터베이스 범위 자격 증명 개체를 만들어 각 Hadoop 사용자에 대해 인증 정보를 지정합니다. [PolyBase T-SQL 개체](../../relational-databases/polybase/polybase-t-sql-objects.md)를 참조하세요.  
  
## <a name="next-steps"></a>다음 단계  
 [PolyBase T-SQL 개체](../../relational-databases/polybase/polybase-t-sql-objects.md)  
  
 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 연결 구성 &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)   
 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)  
  
  