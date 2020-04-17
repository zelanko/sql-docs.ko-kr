---
title: AdventureWorks 샘플 데이터베이스 설치 및 구성
description: 다음 지침에 따라 SQL Server 관리 스튜디오 또는 Azure SQL Database에서 AdventureWorks 샘플 데이터베이스를 다운로드하고 설치합니다.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 7fa3d199450750a444f2b67ae3e4583549d449b9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484582"
---
# <a name="adventureworks-installation-and-configuration"></a>어드벤처웍스 설치 및 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

어드벤처웍스는 링크와 설치 지침을 다운로드합니다. 

## <a name="prerequisites"></a>사전 요구 사항

- [SQL 서버](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 또는 [Azure SQL 데이터베이스](https://azure.microsoft.com/services/sql-database/). 전체 버전의 샘플에서는 SQL 서버 평가/개발자/엔터프라이즈 버전을 사용합니다.
- [SQL 서버 관리 스튜디오](../ssms/download-sql-server-management-studio-ssms.md). 최상의 결과를 얻으려면 2016년 6월 릴리스 또는 그 이후를 사용하십시오.
 
## <a name="oltp-downloads"></a>OLTP 다운로드

어드벤처 웍스의 OLTP 버전에 대한 직접 링크는 아래에서 찾을 수 있습니다 :

- [어드벤처웍스2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [어드벤처웍스2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [어드벤처웍스2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [어드벤처웍스2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [어드벤처웍스2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>데이터 웨어하우스 다운로드

AdventureWorks의 데이터 웨어하우스 버전에 대한 직접 링크는 아래에서 확인할 수 있습니다.

- [어드벤처웍스DW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [어드벤처웍스DW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [어드벤처웍스DW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [어드벤처웍스DW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [어드벤처웍스DW2008R2.bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak)

## <a name="creation-scripts"></a>스크립트 작성
아래 스크립트는 버전에 관계없이 전체 AdventureWorks 데이터베이스를 만드는 데 사용할 수 있습니다. 

- [어드벤처웍스 OLTP 스크립트 지퍼](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [어드벤처웍스 DW 스크립트 지퍼](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>GitHub 링크

- [SQL 2014 - 2016에 대한 모든 어드벤처 웍스 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012에 대한 모든 어드벤처 웍스 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL 2008 및 2008R2에 대한 모든 어드벤처 웍스 파일](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>SQL 서버에 설치

### <a name="restore-backup"></a>백업 복원
SQL Server 관리 스튜디오를 사용하여 데이터베이스 백업을 복원하려면 아래 단계에 따라 

1. SQL Server 관리 Studio를 열고 대상 SQL Server 인스턴스에 연결합니다.
2. 데이터베이스 노드를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원을** **선택합니다.**
3. **장치를** 선택하고 타원을 클릭합니다 **(...**)
4. 대화 상자 백업 **장치 선택에서** **추가를**클릭하고 서버의 파일 시스템에서 데이터베이스 백업으로 이동한 다음 백업을 선택합니다. **확인**을 클릭합니다.
5. 필요한 경우 **파일** 창에서 데이터 및 로그 파일의 대상 위치를 변경합니다. 데이터를 배치하고 파일을 다른 드라이브에 기록하는 것이 좋습니다.
6. **확인**을 클릭합니다. 그러면 데이터베이스 복원이 시작됩니다. 완료되면 SQL Server 인스턴스에 AdventureWorks 데이터베이스가 설치됩니다.

SQL Server 데이터베이스 복원에 대한 자세한 내용은 [SSMS를 사용하여 데이터베이스 백업 복원을](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)참조하십시오.


### <a name="attach-a-datafile"></a>데이터 파일 첨부
SQL Server 관리 스튜디오를 사용하여 데이터베이스에 대한 데이터 파일을 첨부하려면 아래 단계를 따릅니다.

1. SQL Server 관리 Studio를 열고 대상 SQL Server 인스턴스에 연결합니다.
2. **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭하고 **연결**을 선택합니다.
3. **추가를** 선택하고 로 이동합니다. 첨부할 MDF 파일입니다. 
1. 파일을 선택하고 **확인**을 클릭합니다. 
    1. 선택한 데이터베이스가 아래쪽 창에 표시되어야 합니다. 파일이 "찾을 수 없습니다"로 나열된 경우 파일 **...** 이름 옆에 있는 타원(... ) 을 선택하고 경로를 올바른 경로로 업데이트합니다. 
    1. 로그 파일(.ldf)이 아닌 데이터 파일(.mdf)만 있는 경우 아래쪽 창에서 .ldf를 강조 표시하고 **제거를**선택합니다. 그러면 새 로그 파일이 생성됩니다. 
1. **확인을** 선택하여 파일을 첨부합니다. 파일이 첨부되면 SQL Server 인스턴스에 AdventureWorks 데이터베이스가 설치됩니다.  

데이터베이스 파일 첨부에 대한 자세한 내용은 [데이터베이스 첨부](../relational-databases/databases/attach-a-database.md)를 참조하십시오. 

## <a name="install-to-azure-sql-database"></a>Azure SQL 데이터베이스에 설치


Azure에 아직 SQL Server가 없는 경우 [Azure 포털로](https://portal.azure.com/) 이동하여 새 SQL Database를 만듭니다. 데이터베이스를 만드는 과정에서 서버를 만듭니다. 서버를 기록해 둡을 기록합니다. 몇 분 안에 데이터베이스를 만들려면 [이 자습서를](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) 참조하십시오.

1. Azure 포털에 연결합니다.
1. 탐색 창의 왼쪽 상단에 **있는 리소스 만들기를** 선택합니다. 
1. **데이터베이스**를 선택한 다음, **SQL Database**를 선택합니다. 
1. 요청된 정보를 입력합니다.
1. 소스 **선택** 필드에서 **샘플(AdventureWorksLT)을** 선택하여 최신 AdventureWorksLT 백업을 복원합니다.
1. AdventureWorksLT 데이터베이스의 복원된 복사본인 새 SQL 데이터베이스를 **만들려면 만들기를** 선택합니다. 


## <a name="see-also"></a>참고 항목
[SQL 서버 관리 스튜디오에 대한 자습서](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server 데이터베이스 엔진에 대한 자습서](../relational-databases/database-engine-tutorials.md)
