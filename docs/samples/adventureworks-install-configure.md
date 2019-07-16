---
title: 설치 및 AdventureWorks 예제 데이터베이스-SQL 구성 | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 99cdd6fdf5db075cc8fd46b738f468fd5d9a028d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894924"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 설치 및 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 링크와 설치 지침은 다운로드 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 나 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)합니다. 샘플의 전체 버전의 경우 SQL Server 평가/개발자/Enterprise Edition을 사용 합니다.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과 사용 하 여 2016 년 6 월 릴리스 이상.
 
## <a name="github-links"></a>Github 링크

- [SQL 2014 2016에 대 한 모든 AdventureWorks 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012에 대 한 모든 AdventureWorks 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL 2008 및 2008 r2에 대 한 모든 AdventureWorks 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>OLTP 다운로드

아래 AdventureWorks OLTP 버전에 대 한 직접 링크를 찾을 수 있습니다.

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>데이터 웨어하우스 다운로드

아래 AdventureWorks 데이터 웨어하우스 버전에 대 한 직접 링크를 찾을 수 있습니다.

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>생성 스크립트
스크립트 아래 버전에 관계 없이 전체 AdventureWorks 데이터베이스를 만들려면 사용할 수 있습니다. 

- [AdventureWorks OLTP Zip 스크립트](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 스크립트 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>SQL server 설치

### <a name="restore-backup"></a>백업 복원
수행 된 SQL Server Management Studio를 사용 하 여 데이터베이스의 백업을 복원 하려면 다음 단계입니다. 

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드를 선택한 **Restore Database**합니다.
3. 선택 **장치** 줄임표를 클릭 하 고 ( **...** )
4. 대화 상자에서 **백업 장치 선택**, 클릭 **추가**, 서버의 파일 시스템에서 데이터베이스 백업으로 이동 하 고 백업을 선택 합니다. **확인**을 클릭합니다.
5. 필요한 경우 데이터에 대 한 대상 위치를 변경 하 고 로그 파일에는 **파일** 창입니다. 데이터 배치 하 고 여러 드라이브의 로그 파일에 대 한 모범 사례는 note 합니다.
6. **확인**을 클릭합니다. 데이터베이스 복원이 시작 됩니다. 완료 되 면 AdventureWorks 데이터베이스를 SQL Server 인스턴스에 설치 해야 합니다.

SQL Server 데이터베이스 복원에 대 한 자세한 내용은 참조 하세요. [SSMS를 사용 하 여 데이터베이스 백업 복원](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)합니다.


### <a name="attach-a-datafile"></a>연결 된 데이터 파일
수행 된 SQL Server Management Studio를 사용 하 여 데이터베이스에 대 한 데이터 파일을 연결 하려면 다음 단계입니다.

1. SQL Server Management Studio를 열고 대상 SQL Server 인스턴스에 연결 합니다.
2. 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 노드를 선택한 **연결**합니다.
3. 선택 **추가** 로 이동 합니다. 연결 하려는 MDF 파일입니다. 
1. 파일을 선택 하 고 클릭 **확인**합니다. 
    1. 아래쪽 창에 선택한 데이터베이스를 표시 합니다. 파일 나열 되는 경우 "not found"으로 줄임표를 선택 합니다. ( **...** ) 업데이트 하 여 올바른 경로에 대 한 경로 및 파일 이름 옆에 있습니다. 
    1. 하나만 있는 경우 데이터 파일 (.mdf), 및는 로그 파일 (.ldf)을 다음.ldf 아래쪽 창에 강조 표시 및 선택 **제거**합니다. 이렇게 하면 새 로그 파일이 만들어집니다. 
1. 선택 **확인** 파일을 연결 합니다. 파일 연결 된 후에 AdventureWorks 데이터베이스를 SQL Server 인스턴스에 설치 해야 합니다.  

데이터베이스 파일 연결에 대 한 자세한 내용은 참조 하세요. [데이터베이스를 연결할](../relational-databases/databases/attach-a-database.md)합니다. 

## <a name="install-to-azure-sql-database"></a>Azure SQL Database로 설치


수행 하지 아직 있는 경우 SQL Server Azure를 이동할 합니다 [Azure portal](https://portal.azure.com/) 새 SQL 데이터베이스를 만듭니다. 데이터베이스 만들기, 서버를 만듭니다. 서버를 기록해 둡니다. 참조 [이 자습서](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 분 후에는 데이터베이스를 만들려고 합니다.

1. Azure portal에 연결 합니다.
1. 선택 **리소스 만들기** 에서 맨 왼쪽 탐색 창입니다. 
1. 선택 **데이터베이스** 선택한 후 **SQL Database**합니다. 
1. 요청 된 정보를 입력 합니다.
1. 에 **원본 선택** 필드에 선택 **샘플 (AdventureWorksLT)** 최신 AdventureWorksLT 백업의 백업을 복원 하려면.
1. 선택 **만들기** AdventureWorksLT 데이터베이스의 복원 된 복사본 인 새 SQL 데이터베이스를 만들려고 합니다. 


## <a name="see-also"></a>참조
[SQL Server Management Studio에 대 한 자습서](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server 데이터베이스 엔진에 대 한 자습서](../relational-databases/database-engine-tutorials.md)
