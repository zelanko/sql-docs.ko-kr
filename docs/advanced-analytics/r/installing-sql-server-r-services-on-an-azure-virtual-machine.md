---
title: "Azure 가상 컴퓨터에서 SQL Server 컴퓨터 학습 기능을 설치 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0c4b8ef73f4afbc54d2fc1841e281afd0342cedf
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2017
---
# <a name="installing-sql-server-machine-learning-features-on-an-azure-virtual-machine"></a>Azure 가상 컴퓨터에서 기능을 학습 하는 SQL Server 컴퓨터 설치
 
포함 된 Azure 가상 컴퓨터를 배포 하는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 기계 학습의 VM이 만들어지면 인스턴스에 추가할 기능으로 선택할 수 있습니다.

+ [SQL Server 2016 및 R 서비스를 포함 하는 새 VM 만들기](#new)
+ [SQL Server 2016으로 기존 가상 컴퓨터에 시스템 학습 기능을 추가 합니다.](#existing)

> [!NOTE]
> 가상 컴퓨터를 이제 SQL Server 2017 수! 참조 [이 알림은](https://azure.microsoft.com/blog/announcing-new-azure-vm-images-sql-server-2017-on-linux-and-windows/) 대 한 자세한 내용은 합니다.
> 
> R에서 Azure SQL 데이터베이스 미리 보기 기능으로 사용할 수도 있습니다. 자세한 내용은 참조 [Azure SQL 데이터베이스에서 사용 하 여 R](../r/using-r-in-azure-sql-database.md)합니다.

## <a name="create-a-new-sql-server-2017-virtual-machine"></a>새 SQL Server 2017 가상 컴퓨터 만들기

Python 또는 R에서 SQL Server 2017을 사용 하려면 Windows 기반 가상 컴퓨터를 구입 해야 합니다. [!INCLUDE[sscurrentlong-md](../../includes/sscurrentlong-md.md)]linux 지원 빠른 [기본 점수 매기기](../sql-native-scoring.md) 사용할 수 없는 기능을 학습 하는 다른 컴퓨터에서 T-SQL 예측 함수를 사용 하 여이 버전에서는 아직 합니다.

SQL Server VM 제품 목록은이 문서를 참조: [개요 SQL Server의 Azure 가상 컴퓨터 (Windows)에서](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)합니다.

### <a name="new"></a>기계 학습에서 새로운 SQL Server Enterprise VM 만들기

1. Azure 포털에서 가상 컴퓨터를 클릭 한 다음 새로 만들기를 클릭 합니다.
2. SQL Server 2017 Enterprise Edition을 선택 합니다.
3. 서버 이름 및 계정 권한을 구성하고 요금제를 선택합니다.
4. **SQL Server 설정** (VM 설치 마법사의 단계 4)를 찾을 **컴퓨터 학습 서비스 (고급 분석)** 클릭 **사용**합니다.
5. 유효성 검사를 위해 제공된 요약을 검토하고 **확인**을 클릭합니다.
6. 가상 컴퓨터가 준비되면 가상 컴퓨터에 연결하고 미리 설치된 SQL Server Management Studio를 엽니다. 기계 학습을 실행 하도록 준비 합니다.
7. 이를 확인하려면 새 쿼리 창을 열고 R을 사용하여 1~10의 숫자 시퀀스를 생성하는 다음과 같은 간단한 문을 실행합니다.

    ```
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
    ```

6. 원격 데이터 과학 클라이언트에서 인스턴스에 연결 하려는 경우 완료 [추가 단계](#additional-steps) 필요에 따라 합니다.

### <a name="disable-machine-learning-features-on-a-sql-server-vm"></a>SQL Server VM에서 컴퓨터 학습 기능을 사용 하지 않도록 설정

사용 하도록 설정 하거나 언제 든 지 기존 SQL Server 가상 컴퓨터에서이 기능을 비활성화할 수 있습니다.

1. 가상 컴퓨터 블레이드를 엽니다.
2. **설정**을 클릭하고 **SQL Server 구성**을 선택합니다.
3. 기능을 변경 하 고 적용 합니다.

### <a name="existing"></a>기존 SQL Server 2016 Enterprise VM R 서비스 추가합니다

기계 학습 하지 않고 SQL Server를 포함 하는 Azure 가상 컴퓨터를 만든 경우 다음이 단계를 수행 하 여 기능을 추가할 수 있습니다.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 다시 실행하고 마법사의 **서버 구성** 페이지에서 기능을 추가합니다.
2. 외부 스크립트 실행을 사용하도록 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 다시 시작합니다. 자세한 내용은 참조 [SQL Server R Services 설치](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)합니다.
3. (선택 사항) 원격 스크립트 실행에 필요한 경우 R 작업자 계정에 대한 데이터베이스 액세스를 구성합니다.
   자세한 내용은 [SQL Server R Services 설정](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)을 참조하세요.
3. (선택 사항) 원격 데이터 과학 클라이언트에서 R 스크립트 실행을 허용하려면 Azure 가상 컴퓨터에서 방화벽 규칙을 수정합니다. 자세한 내용은 [방화벽 차단 해제](#firewall)를 참조하세요.
4. 필요한 네트워크 라이브러리를 설치하거나 사용하도록 설정합니다. 자세한 내용은 [네트워크 프로토콜 추가](#network)를 참조하세요.

## <a name="additional-steps"></a>추가 단계

원격 클라이언트가 SQL Server 계산 컨텍스트를 원격으로 서버에 액세스할 수를 예상 되는 경우에 몇 가지 추가 단계가 필요 합니다.

### <a name="firewall"></a>방화벽 차단 해제

기본적으로 Azure 가상 컴퓨터의 방화벽이 네트워크 로컬 사용자 계정에 대 한 액세스를 차단 하는 규칙을 포함 합니다.

이 규칙에 액세스할 수 있는지 확인을 사용 하지 않도록 설정 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 데이터 과학 클라이언트에서 인스턴스.  그렇지 않으면 기계 학습 코드는 가상 컴퓨터의 작업 영역을 사용 하는 계산 컨텍스트를 실행할 수 없습니다.

원격 데이터 과학 클라이언트에서 액세스할 수 있도록 합니다.

1. 가상 컴퓨터에서 고급 보안이 포함된 Windows 방화벽을 엽니다.
2. **아웃바운드 규칙**을 선택합니다.
3. 다음 규칙을 사용하지 않도록 설정합니다.
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>원격 클라이언트에 대한 ODBC 콜백 사용

예상 되는 서버를 호출 하는 클라이언트 솔루션을 학습 하는 컴퓨터의 일부로 ODBC 쿼리를 실행 해야 합니다는 실행 패드 원격 클라이언트를 대신 하 여 ODBC 호출을 수행할 수 있는지 확인 해야 합니다. 이 작업을 하려면 실행 패드에서 사용되는 SQL 작업자 계정이 인스턴스에 로그인하도록 허용해야 합니다.
자세한 내용은 [SQL Server R Services 설정](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)을 참조하세요.

### <a name="network"></a>네트워크 프로토콜 추가

+ 명명된 파이프 사용
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 클라이언트와 서버 컴퓨터 간의 연결 및 일부 인터넷 연결을 위해 명명된 파이프 프로토콜을 사용합니다. 명명된 파이프를 사용하지 않는 경우 Azure 가상 컴퓨터 및 서버에 연결된 데이터 과학 클라이언트에서 둘 다 명명된 파이프를 설치하고 사용하도록 설정해야 합니다.
  
+ TCP/IP 사용

  TCP/IP는 루프백 연결에 필요 합니다. 다음과 같은 오류가 발생할 경우 인스턴스를 지 원하는 가상 컴퓨터에서 TCP/IP를 설정 합니다.

  "DBNETLIB; SQL Server가 없거나 액세스가 거부 되었습니다 "

## <a name="related-resources"></a>관련 리소스

[Azure SQL 데이터베이스에서 R을 사용 하 여](../r/using-r-in-azure-sql-database.md)