---
title: 추가 및 제거 Access 데이터베이스 파일 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fc44607d172ebc1f8d7d09b68ba77d68002de2bb
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Access 데이터베이스 파일 (AccessToSQL) 추가 및 제거
로 Access 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure SSMA 프로젝트에 하나 이상의 Access 데이터베이스를 추가 해야 합니다. 이러한 데이터베이스는 Access 97 또는 이후 버전 이어야 합니다. 데이터베이스를 이전 버전의 Access가 최신 버전으로 데이터베이스를 변환 해야 합니다. 열고 SSMA를 추가 하기 전에 Access 97 또는 이후 버전에서 데이터베이스를 저장 하 여이 작업을 수행 합니다.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Access 데이터베이스 파일을 추가 하면 어떻게 되나요?  
SSMA 프로젝트에 Access 데이터베이스를 추가 하면 SSMA는 데이터베이스 메타 데이터를 읽고 프로젝트 파일을이 메타 데이터를 추가 합니다. 이 메타 데이터는 데이터베이스와 해당 개체를 설명합니다. SSMA는 개체를 변환 하는 경우 메타 데이터 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 구문이 데이터를 마이그레이션할 때와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다. 액세스 메타 데이터 탐색기에서이 메타 데이터를 찾아볼 수 있으며 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!NOTE]  
> Access 데이터베이스를 여러 파일로 분할할 수 있습니다: 테이블을 포함 하는 백 엔드 데이터베이스와 쿼리, 폼, 보고서, 매크로, 모듈 및 바로 가기 키를 포함 하는 프런트 엔드 데이터베이스입니다. 데이터베이스를 분할 하려는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure, SSMA에 프런트 엔드 데이터베이스를 추가 합니다.  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA에 필요한 사용 권한  
Access 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure, 사용자 그룹 및 관리자 사용자는 관리 권한이 있어야 합니다. 작업 그룹 보호를 사용 하 여 데이터베이스를 마이그레이션하는 방법에 대 한 정보를 참조 하세요. [마이그레이션에 대 한 Access 데이터베이스 준비](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
## <a name="selecting-databases-to-add"></a>데이터베이스를 추가 하려면 선택  
SSMA 프로젝트에 하나 이상의 데이터베이스를 추가 하려는 경우 파일은 모두 한 알려진된 위치에서에서 다음 절차를 사용 하 여 파일을 추가할 수 있습니다.  
  
**개별 데이터베이스 파일을 추가 하려면**  
  
1.  에 **파일** 메뉴를 클릭 하 여 **추가 데이터베이스**합니다.  
  
2.  에 **열려** 대화 상자에서 데이터베이스 파일 또는 파일에 포함 된 폴더를 찾습니다.  
  
3.  파일을 추가 하 고 클릭 하려는 선택 **열려**합니다.  
  
## <a name="finding-databases-to-add"></a>데이터베이스를 추가 하려면 찾기  
SSMA 프로젝트에 서로 다른 폴더에서 여러 개의 Access 데이터베이스를 추가 하려면 파일을 찾을 수 있는데 단일 파일을 추가 하려는 경우 더 많은 파일 중 하나를 찾아 프로젝트에 추가 하려면 다음이 단계를 수행 합니다.  
  
**찾아 데이터베이스를 추가 합니다.**  
  
1.  에 **파일** 메뉴를 클릭 하 여 **찾을 데이터베이스**합니다.  
  
2.  데이터베이스 검색 마법사에는 드라이브, 파일 경로 또는 검색할 UNC 경로의 이름을 입력 합니다. 또는 클릭 하 여 **찾아보기** 드라이브 또는 네트워크 폴더를 찾습니다.  
  
3.  클릭 **추가** 위치 목록에 추가 합니다.  
  
    자세한 검색 위치를 추가 하려면 이전 두 단계를 반복 합니다.  
  
4.  필요에 따라 반환 되는 데이터베이스의 목록을 구체화 하려면 검색 조건을 추가 합니다.  
  
    > [!IMPORTANT]  
    > **전체 또는 일부 파일 이름의** 입력란 와일드 카드 문자를 지원 하지 않습니다.  
  
5.  클릭 **스캔**합니다.  
  
    검색 페이지가 표시 됩니다. 여기에 발견 된 데이터베이스 및 검색 진행률 표시. 검색을 중지 하려면 클릭 **중지**합니다.  
  
6.  파일 선택 페이지에서 데이터베이스 프로젝트에 추가 하려면를 선택 합니다.  
  
    사용할 수는 **모두 선택** 및 **모두 지우기** 선택 하거나 모든 데이터베이스를 선택 취소 하는 목록의 위쪽에 있는 단추입니다. 아래로 데이터베이스의 범위를 선택 하 고 SHIFT 키 또는 여러 데이터베이스를 선택 하려면 CTRL 키를 누른 수 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  확인 페이지에서 클릭 **마침**합니다.  
  
## <a name="browsing-access-metadata"></a>액세스 메타 데이터 찾아보기  
Access 데이터베이스 프로젝트에 추가한 후 프로젝트 메타 데이터 액세스 메타 데이터 탐색기에 나타납니다. 데이터베이스 및 데이터베이스 개체 탐색기에서의 계층 구조를 찾아볼 수 있습니다.  
  
**메타 데이터를 찾아보려면**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스 메타 베이스**을 펼친 다음 **데이터베이스**합니다.  
  
2.  데이터베이스를 검토 한 다음를 확장 하려면 확장 **쿼리**합니다.  
  
    쿼리의 목록을 확인 합니다. 쿼리를 선택 하는 경우는 **SQL** 탭 및 **속성** 탭이 오른쪽 창에 표시 합니다.  
  
3.  확장 **테이블** 다음 테이블을 선택 합니다.  
  
    4 개의 탭 표시: **테이블**, **유형 매핑**, **속성**, 및 **데이터**합니다.  
  
4.  테이블을 확장 하 고 **키**, 한 다음 키를 선택 합니다.  
  
    키 속성 오른쪽 창에 나타납니다.  
  
5.  확장 **인덱스**, 한 다음 인덱스를 선택 합니다.  
  
    인덱스 속성 오른쪽 창에 나타납니다.  
  
## <a name="refreshing-databases"></a>데이터베이스를 새로 고침  
Access 데이터베이스의 파일을 추가한 후 변경 되는 경우 Access 데이터베이스의 메타 데이터를 업데이트할 수 있습니다.  
  
**액세스 메타 데이터를 업데이트 하려면**  
  
-   액세스 메타 데이터 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터베이스에서 새로 고침**합니다.  
  
## <a name="removing-databases"></a>데이터베이스 제거  
다음이 단계를 수행 하 여 프로젝트에서 Access 데이터베이스를 제거할 수 있습니다.  
  
**프로젝트에서 데이터베이스를 제거 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스 메타 베이스**을 펼친 다음 **데이터베이스**합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 선택 **데이터베이스 제거**합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계에서는 [SQL Server에 연결](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[프로젝트 만들기 및 관리](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)  
  
