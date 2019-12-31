---
title: AdventureWorks 예제 데이터베이스 설치 및 구성
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 6a4b56a31ede0d8e011c1a2244f5d014e185e7e5
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74318992"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 설치 및 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 다운로드 링크 및 설치 지침을 참조 하세요. 

## <a name="prerequisites"></a>필수 구성 요소

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 또는 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). 샘플의 전체 버전은 SQL Server Evaluation/Developer/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과를 위해 6 월 2016 릴리스 이상을 사용 합니다.
 
## <a name="oltp-downloads"></a>OLTP 다운로드

AdventureWorks의 OLTP 버전에 대 한 직접 링크는 아래에서 찾을 수 있습니다.

- [AdventureWorks2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>데이터 웨어하우스 다운로드

AdventureWorks의 데이터 웨어하우스 버전에 대 한 직접 링크는 아래에서 찾을 수 있습니다.

- [AdventureWorksDW2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>작성 스크립트
아래 스크립트를 사용 하 여 버전과 관계 없이 전체 AdventureWorks 데이터베이스를 만들 수 있습니다. 

- [AdventureWorks OLTP 스크립트 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 스크립트 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>GitHub 링크

- [SQL 2014-2016의 모든 AdventureWorks 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012에 대 한 모든 AdventureWorks 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [모든 AdventureWorks 파일 (SQL 2008 및 2008 R2)](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>SQL Server에 설치

### <a name="restore-backup"></a>백업 복원
다음 단계에 따라 SQL Server Management Studio를 사용 하 여 데이터베이스의 백업을 복원 합니다. 

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스 복원**을 선택 합니다.
3. **장치** 를 선택 하 고 줄임표 (**...**)를 클릭 합니다.
4. 대화 상자에서 **백업 장치를 선택**하 고, **추가**를 클릭 하 고, 서버의 파일 시스템에 있는 데이터베이스 백업으로 이동 하 고, 백업을 선택 합니다. 
  **확인**을 클릭합니다.
5. 필요한 경우 **파일** 창에서 데이터 및 로그 파일의 대상 위치를 변경 합니다. 데이터와 로그 파일을 서로 다른 드라이브에 저장 하는 것이 가장 좋습니다.
6. 
  **확인**을 클릭합니다. 그러면 데이터베이스 복원이 시작 됩니다. 완료 되 면 AdventureWorks 데이터베이스가 SQL Server 인스턴스에 설치 됩니다.

SQL Server 데이터베이스 복원에 대 한 자세한 내용은 SSMS를 [사용 하 여 데이터베이스 백업 복원](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)을 참조 하세요.


### <a name="attach-a-datafile"></a>데이터 데이터 연결
다음 단계에 따라 SQL Server Management Studio를 사용 하 여 데이터베이스에 대 한 데이터 데이터를 연결 합니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **연결**을 선택 합니다.
3. **추가** 를 선택 하 고로 이동 합니다. 연결 하려는 MDF 파일입니다. 
1. 파일을 선택하고 **확인**을 클릭합니다. 
    1. 선택한 데이터베이스는 아래쪽 창에 표시 됩니다. 파일이 "찾을 수 없음"으로 표시 되는 경우 파일 이름 옆에 있는 줄임표 (**...**)를 선택 하 고 경로를 올바른 경로로 업데이트 합니다. 
    1. 로그 파일 (.ldf)이 아닌 데이터 파일 (.mdf)만 있는 경우 맨 아래 창에서 .ldf를 강조 표시 하 고 **제거**를 선택 합니다. 그러면 새 로그 파일이 생성 됩니다. 
1. **확인** 을 선택 하 여 파일을 첨부 합니다. 파일이 연결 된 후에는 SQL Server 인스턴스에 AdventureWorks 데이터베이스가 설치 됩니다.  

데이터베이스 파일 연결에 대 한 자세한 내용은 [데이터베이스 연결](../relational-databases/databases/attach-a-database.md)을 참조 하세요. 

## <a name="install-to-azure-sql-database"></a>Azure SQL Database에 설치


Azure에 아직 SQL Server 없는 경우 [Azure Portal](https://portal.azure.com/) 로 이동 하 여 새 SQL Database를 만듭니다. 데이터베이스를 만드는 과정에서 서버를 만듭니다. 서버를 기록해 둡니다. 몇 분만에 데이터베이스를 만들려면 [이 자습서](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 를 참조 하세요.

1. Azure Portal에 연결 합니다.
1. 탐색 창의 왼쪽 위에서 **리소스 만들기** 를 선택 합니다. 
1. 
  **데이터베이스**를 선택한 다음, **SQL Database**를 선택합니다. 
1. 요청 된 정보를 입력 합니다.
1. **원본 선택** 필드에서 **Sample (AdventureWorksLT)** 을 선택 하 여 최신 AdventureWorksLT 백업의 백업을 복원 합니다.
1. **만들기** 를 선택 하 여 AdventureWorksLT 데이터베이스의 복원 된 복사본 인 새 SQL Database를 만듭니다. 


## <a name="see-also"></a>참고 항목
[SQL Server Management Studio 자습서](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server 데이터베이스 엔진에 대 한 자습서](../relational-databases/database-engine-tutorials.md)
