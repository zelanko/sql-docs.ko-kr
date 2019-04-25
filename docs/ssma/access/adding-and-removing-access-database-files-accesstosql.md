---
title: 추가 하 고 액세스 권한을 제거 해도 데이터베이스 파일 (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8de9b27a58d277191a4d40da6b34dbcbbd43e497
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62760617"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Access 데이터베이스 파일 (AccessToSQL) 추가 및 제거
로 Access 데이터를 마이그레이션하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure SSMA 프로젝트에 하나 이상의 Access 데이터베이스를 추가 해야 합니다. 이러한 데이터베이스는 Access 97 또는 이후 버전 이어야 합니다. 이전 버전의 Access에서 데이터베이스에 있는 경우 데이터베이스를 최신 버전으로 변환 해야 합니다. 열고 SSMA를 추가 하기 전에 Access 97 이상에서 데이터베이스를 저장 하 여이 작업을 수행 합니다.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Access 데이터베이스 파일을 추가 하면 어떻게 되나요?  
SSMA 프로젝트에 Access 데이터베이스를 추가 하면 SSMA는 데이터베이스 메타 데이터를 읽고 프로젝트 파일에이 메타 데이터를 추가 합니다. 이 메타 데이터 데이터베이스 및 해당 개체를 설명 합니다. SSMA는 개체를 변환할 때 메타 데이터를 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문이 데이터를 마이그레이션한 경우 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다. 액세스 메타 데이터 탐색기에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!NOTE]  
> Access 데이터베이스를 여러 파일로 분할할 수 있습니다: 테이블을 포함 하는 백 엔드 데이터베이스 및 쿼리, 폼, 보고서, 매크로, 모듈 및 바로 가기 키를 포함 하는 프런트 엔드 데이터베이스입니다. 분할 데이터베이스를 마이그레이션할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure, SSMA에 프런트 엔드 데이터베이스를 추가 합니다.  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA에 필요한 사용 권한  
Access 데이터베이스를 마이그레이션하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 사용자 그룹 및 관리자 관리 권한이 있어야 합니다. 작업 그룹 보호를 사용 하 여 데이터베이스를 마이그레이션하는 방법에 대 한 정보를 참조 하세요 [Access 데이터베이스 마이그레이션에 대 한 준비](preparing-access-databases-for-migration-accesstosql.md)합니다.  
  
## <a name="selecting-databases-to-add"></a>추가할 데이터베이스 선택  
SSMA 프로젝트를 하나 이상의 데이터베이스를 추가 하려는 경우 알려진된 한곳에서 모든 파일은 다음 절차를 사용 하 여 파일을 추가할 수 있습니다.  
  
**개별 데이터베이스 파일을 추가 하려면**  
  
1.  에 **파일** 메뉴에서 클릭 **추가 데이터베이스**합니다.  
  
2.  에 **열고** 대화 상자에서 데이터베이스 파일 또는 파일을 포함 하는 폴더를 찾습니다.  
  
3.  파일을 추가 하 고 클릭 하려는 선택 **열려**합니다.  
  
## <a name="finding-databases-to-add"></a>추가할 데이터베이스 찾기  
SSMA 프로젝트를 다른 폴더에서 여러 Access 데이터베이스를 추가 하려는 경우 파일을 찾을 수 없지만 단일 파일을 추가 하려는 파일 하나 이상 찾아 프로젝트에 추가 하려면 다음이 단계를 수행 합니다.  
  
**찾아 데이터베이스를 추가 합니다.**  
  
1.  에 **파일** 메뉴에서 클릭 **찾을 데이터베이스**합니다.  
  
2.  데이터베이스 찾기 마법사에서 드라이브, 파일 경로 또는 UNC 경로 검색 하려는의 이름을 입력 합니다. 를 클릭할 **찾아보기** 드라이브 또는 네트워크 폴더를 찾습니다.  
  
3.  클릭 **추가** 위치 목록에 추가 합니다.  
  
    더 많은 검색 위치를 추가 하는 이전 두 단계를 반복 합니다.  
  
4.  필요에 따라 반환 되는 데이터베이스의 목록을 구체화 하려면 검색 조건을 추가 합니다.  
  
    > [!IMPORTANT]  
    > 합니다 **파일 이름의 일부나 전부** 입력란 와일드 카드 문자를 지원 하지 않습니다.  
  
5.  클릭 **스캔**합니다.  
  
    검색 페이지가 표시 됩니다. 검색 된 데이터베이스 및 검색의 진행률 표시 됩니다. 검색을 중지 하려면 클릭 **중지**합니다.  
  
6.  파일 선택 페이지에서 프로젝트에 추가 하려는 데이터베이스를 선택 합니다.  
  
    사용할 수는 **모두 선택** 하 고 **모두 지우기** 선택 하거나 모든 데이터베이스를 선택 취소 목록의 맨 위에 있는 단추입니다. 여러 데이터베이스를 선택 하려면 CTRL 키를 길게 누른 또는 데이터베이스 범위 선택으로 SHIFT 키를 누른 채로 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  확인 페이지에서 클릭 **완료**합니다.  
  
## <a name="browsing-access-metadata"></a>메타 데이터에 액세스를 검색합니다.  
프로젝트에 Access 데이터베이스를 추가한 후 프로젝트 메타 데이터 액세스 메타 데이터 탐색기에 나타납니다. 데이터베이스 및 데이터베이스 개체 탐색기에서 계층 구조를 찾아볼 수 있습니다.  
  
**메타 데이터를 찾아보려면**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스-메타 베이스**를 차례로 확장 하 고 **데이터베이스**합니다.  
  
2.  를 검토 한 다음를 확장 하려는 데이터베이스를 확장 **쿼리**합니다.  
  
    쿼리의 목록을 확인할 수 있습니다. 쿼리를 선택 하는 경우는 **SQL** 탭 및 **속성** 탭이 오른쪽 창에 표시 합니다.  
  
3.  확장 **테이블** 다음 테이블을 선택 합니다.  
  
    4 개의 탭이 표시 되는지 확인 합니다. **테이블**, **형식 매핑**합니다 **속성**, 및 **데이터**입니다.  
  
4.  테이블을 확장 하 고 **키**, 한 다음 키를 선택 합니다.  
  
    키 속성이 오른쪽 창에 나타납니다.  
  
5.  확장 **인덱스**, 한 다음 인덱스를 선택 합니다.  
  
    인덱스 속성 오른쪽 창에 나타납니다.  
  
## <a name="refreshing-databases"></a>데이터베이스를 새로 고침  
Access 데이터베이스에 해당 파일을 추가한 후 변경 될 경우에 Access 데이터베이스의 메타 데이터를 업데이트할 수 있습니다.  
  
**메타 데이터에 액세스를 업데이트 하려면**  
  
-   액세스 메타 데이터 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택한 **데이터베이스에서 새로 고침**합니다.  
  
## <a name="removing-databases"></a>데이터베이스를 제거합니다.  
다음이 단계를 수행 하 여 프로젝트에서 Access 데이터베이스를 제거할 수 있습니다.  
  
**프로젝트에서 데이터베이스를 제거 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스-메타 베이스**를 차례로 확장 하 고 **데이터베이스**합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 선택한 **Remove Database**합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스에서 다음 단계 [SQL Server에 연결](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[프로젝트 만들기 및 관리](creating-and-managing-projects-accesstosql.md)  
  
