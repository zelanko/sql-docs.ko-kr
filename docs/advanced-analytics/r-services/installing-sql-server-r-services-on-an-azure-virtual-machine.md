---
title: "Azure 가상 컴퓨터에 SQL Server R 서비스 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Azure 가상 컴퓨터에 SQL Server R 서비스 설치
 
포함 된 Azure 가상 컴퓨터를 배포 하는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], R 서비스 VM에 만들어질 때 인스턴스에 추가할 기능으로 선택할 수 있습니다. 



+ [SQL Server 2016 및 R 서비스를 사용 하 여 새 VM 만들기](#new)
+ [SQL Server 2016으로 기존 가상 컴퓨터에 R 서비스 추가](#existing)

## <a name="a-namenewacreate-a-new-sql-server-2016-enterprise-virtual-machine-with-r-services-enabled"></a><a name="new"></a>R 서비스가 사용 하도록 설정 된 새 SQL Server 2016 엔터프라이즈 가상 컴퓨터 만들기

1. Azure 포털에서 가상 컴퓨터를 클릭 한 다음 새로 만들기를 클릭 합니다.
2. SQL Server 2016 Enterprise Edition을 선택 합니다.
3. 서버 이름 및 계정 권한을 구성 하 고 가격 계획을 선택 합니다.
4. 설치 마법사, VM의 4 단계에서 **SQL Server 설정**, 찾습니다 **R 서비스 (고급 분석)** 클릭 **사용**합니다.
5. 유효성 검사 및 클릭에 대 한 표시 요약 검토 **확인**합니다.
6. 가상 컴퓨터 준비 되 면에 연결 하 고은 사전 설치 되어 있는 SQL Server Management Studio를 엽니다. R 서비스를 실행할 준비가 되었습니다. 
7. 이 확인 하려면 새 쿼리 창을 열고 R을 사용 하 여 1에서 10 일련의 숫자를 생성 하는 다음과 같은 간단한 문을 실행 합니다.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. 원격 데이터 과학 클라이언트에서 인스턴스에 연결 합니다, 완료 [추가 단계](#additional-steps) 필요에 따라 합니다.


## <a name="additional-steps"></a>추가 단계  

원격 클라이언트를 원격 SQL Server 계산 컨텍스트는 서버에 액세스 하 려 할 경우 R 서비스를 사용 하 여 몇 가지 추가 단계가 필요할 수 있습니다.

### <a name="a-namefirewallaunblock-the-firewall"></a><a name="firewall"></a>방화벽을 차단 해제  
  
액세스할 수 있는지 확인 하려면 가상 컴퓨터에서 방화벽 규칙을 변경 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 데이터 과학 클라이언트에서 인스턴스.  그렇지 않으면 가상 컴퓨터의 작업 영역을 필요로 하는 컨텍스트를 사용 하는 compute 절을 사용할 수 없습니다. 

기본적으로 Azure 가상 컴퓨터의 방화벽이 네트워크 로컬 R 사용자 계정에 대 한 액세스를 차단 하는 규칙을 포함 합니다.  
  
원격 데이터 과학 클라이언트로부터 R 서비스에 대 한 액세스를 설정.
1. 가상 컴퓨터에서 고급 보안이 포함 된 Windows 방화벽을 엽니다.
2. 선택 **아웃 바운드 규칙**
3. 다음 규칙을 사용 하지 않도록 설정 합니다.  
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`  
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>원격 클라이언트에 대 한 ODBC 콜백을 사용 하도록 설정

서버를 호출 하는 R 클라이언트 ODBC 쿼리를 실행 하 고 R 솔루션의 일부로 만들어야 합니다를 려 할 경우 실행 패드 원격 클라이언트를 대신 하 여 ODBC 호출을 설정할 수 있는지 확인 해야 합니다. 이 위해 인스턴스에 로그인 하려면 실행 패드에서 사용 되는 SQL 근로자 계정을 허용 해야 합니다.
자세한 내용은 참조 [설정를 SQL Server R 서비스](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)합니다. 

### <a name="a-namenetworkaadd-network-protocols"></a><a name="network"></a>네트워크 프로토콜을 추가 합니다.  
  
+ 명명 된 파이프 사용
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 일부 내부 연결 하 고 클라이언트와 서버 컴퓨터 간의 연결에 대 한 명명 된 파이프 프로토콜을 사용합니다. 명명 된 파이프를 사용 하지 않는 경우 설치 하 고 서버에 연결 하는 데이터 과학 클라이언트 및 Azure 가상 컴퓨터 모두에서 사용 하도록 설정 해야 합니다.  
  
+ TCP/IP를 사용 하도록 설정

  TCP/IP는 SQL Server R 서비스에 대 한 루프백 연결에 필요 합니다. 다음과 같은 오류가 경우 DBNETLIB; 인스턴스를 지 원하는 가상 컴퓨터에서 TCP/IP 설정 SQL Server가 없거나 액세스가 거부 되었습니다.

## <a name="how-to-disable-r-services-on-an-instance"></a>인스턴스에서 R 서비스를 사용 하지 않도록 설정 하는 방법

사용 하도록 설정 하거나 언제 든 지 기존 가상 컴퓨터에서이 기능을 비활성화할 수 있습니다. 

1. 가상 컴퓨터 블레이드를 열으십시오
2. 클릭 **설정을**, 를 선택 하 고 **SQL Server 구성**합니다.


## <a name="a-nameexistingaadd-sql-server-r-services-to-an-existing-sql-server-2016-enterprise-virtual-machine"></a><a name="existing"></a>기존 SQL Server 2016 Enterprise 가상 컴퓨터에 SQL Server R 서비스 추가

SQL Server 2016 R 서비스를 포함 하지 않는 Azure VM을 만든 경우 다음이 단계를 수행 하 여 기능을 추가할 수 있습니다.

1. 다시 실행 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 및 기능에 추가 된 **서버 구성** 마법사의 페이지입니다.
2. 외부 스크립트의 실행을 사용 하도록 설정 하 고 다시 시작은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스. 자세한 내용은 참조 참조 [설정를 SQL Server R 서비스](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)합니다.
3. (선택 사항) 원격 스크립트 실행에 필요한 경우에 R 작업자 계정에 대 한 데이터베이스 액세스를 구성 합니다.
   자세한 내용은 참조 [설정를 SQL Server R 서비스](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)합니다. 
3. (선택 사항) 원격 데이터 과학 클라이언트에서 R 스크립트 실행을 허용 하려는 경우 Azure 가상 컴퓨터의 방화벽 규칙을 수정 합니다. 자세한 내용은 참조 [방화벽 차단 해제](#firewall)합니다.
4. 설치 또는 필수 네트워크 라이브러리를 사용 하도록 설정 합니다. 자세한 내용은 참조 [네트워크 프로토콜을 추가](#network)합니다.

## <a name="see-also"></a>참고 항목
[Sql Server R 서비스 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)