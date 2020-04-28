---
title: Access 데이터베이스 파일 추가 및 제거 (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 39df13a3cab2d842a313ca37fc4a98d0c331ba83
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68104208"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Access 데이터베이스 파일 추가 및 제거 (AccessToSQL)
액세스 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하려면 ssma 프로젝트에 하나 이상의 access 데이터베이스를 추가 해야 합니다. 이러한 데이터베이스는 97 이상 버전에 액세스 해야 합니다. 이전 버전의 Access에서 데이터베이스를 사용 하는 경우 데이터베이스를 최신 버전으로 변환 해야 합니다. 이렇게 하려면 SSMA에 추가 하기 전에 Access 97 이상 버전에서 데이터베이스를 열고 저장 합니다.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>Access 데이터베이스 파일을 추가 하면 어떻게 되나요?  
SSMA 프로젝트에 Access 데이터베이스를 추가 하는 경우 SSMA는 데이터베이스 메타 데이터를 읽은 다음이 메타 데이터를 프로젝트 파일에 추가 합니다. 이 메타 데이터는 데이터베이스 및 해당 개체에 대해 설명 합니다. SSMA는 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 구문으로 변환 하는 경우와 데이터를 또는 SQL Azure으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 마이그레이션하는 경우 메타 데이터를 사용 합니다. 액세스 메타 데이터 탐색기에서이 메타 데이터를 찾아보고 개별 데이터베이스 개체의 속성을 검토할 수 있습니다.  
  
> [!NOTE]  
> Access 데이터베이스는 테이블이 포함 된 백 엔드 데이터베이스와 쿼리, 폼, 보고서, 매크로, 모듈 및 바로 가기를 포함 하는 프런트 엔드 데이터베이스 등 여러 파일로 분할할 수 있습니다. 분할 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하려면 프런트 엔드 데이터베이스를 ssma에 추가 합니다.  
  
## <a name="permissions-that-are-required-by-ssma"></a>SSMA에 필요한 사용 권한  
Access 데이터베이스를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 마이그레이션하려면 Users 그룹과 Admin 사용자에 게 관리자 권한이 있어야 합니다. 작업 그룹 보호를 사용 하 여 데이터베이스를 마이그레이션하는 방법에 대 한 자세한 내용은 [마이그레이션을 위해 Access 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md)를 참조 하세요.  
  
## <a name="selecting-databases-to-add"></a>추가할 데이터베이스 선택  
SSMA 프로젝트에 하나 이상의 데이터베이스를 추가 하 고 파일이 모두 하나의 알려진 위치에 있는 경우 다음 절차를 사용 하 여 파일을 추가할 수 있습니다.  
  
**개별 데이터베이스 파일을 추가 하려면**  
  
1.  **파일** 메뉴에서 **데이터베이스 추가**를 클릭 합니다.  
  
2.  **열기** 대화 상자에서 데이터베이스 파일이 포함 된 폴더를 찾습니다.  
  
3.  추가 하려는 파일을 선택한 다음 **열기**를 클릭 합니다.  
  
## <a name="finding-databases-to-add"></a>추가할 데이터베이스 찾기  
다른 폴더의 여러 Access 데이터베이스를 SSMA 프로젝트에 추가 하려는 경우 또는 단일 파일을 추가 하 고 파일을 찾아야 하는 경우 다음 단계를 수행 하 여 파일을 하나 더 찾아서 프로젝트에 추가할 수 있습니다.  
  
**데이터베이스를 찾아서 추가 하려면**  
  
1.  **파일** 메뉴에서 **데이터베이스 찾기**를 클릭 합니다.  
  
2.  데이터베이스 찾기 마법사에서 검색할 드라이브의 이름, 파일 경로 또는 UNC 경로를 입력 합니다. 또는 **찾아보기** 를 클릭 하 여 드라이브 또는 네트워크 폴더를 찾습니다.  
  
3.  **추가** 를 클릭 하 여 목록에 위치를 추가 합니다.  
  
    이전 두 단계를 반복 하 여 더 많은 검색 위치를 추가 합니다.  
  
4.  필요에 따라 검색 조건을 추가 하 여 반환 되는 데이터베이스 목록을 구체화 합니다.  
  
    > [!IMPORTANT]  
    > **파일 이름 텍스트 상자의 전체 또는 일부** 는 와일드 카드 문자를 지원 하지 않습니다.  
  
5.  **검색**을 클릭 합니다.  
  
    검색 페이지가 나타납니다. 찾은 데이터베이스와 검색 진행률이 표시 됩니다. 검색을 중지 하려면 **중지**를 클릭 합니다.  
  
6.  파일 선택 페이지에서 프로젝트에 추가 하려는 데이터베이스를 선택 합니다.  
  
    목록의 맨 위에 있는 **모두 선택** 및 **모두 지우기** 단추를 사용 하 여 모든 데이터베이스를 선택 하거나 선택 취소할 수 있습니다. CTRL 키를 누른 채 여러 데이터베이스를 선택 하거나 SHIFT 키를 누른 채 데이터베이스 범위를 선택할 수 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  확인 페이지에서 **마침**을 클릭 합니다.  
  
## <a name="browsing-access-metadata"></a>액세스 메타 데이터 찾아보기  
프로젝트에 Access 데이터베이스를 추가한 후에는 Access Metadata Explorer에 프로젝트 메타 데이터가 표시 됩니다. 탐색기에서 데이터베이스 및 데이터베이스 개체의 계층 구조를 탐색할 수 있습니다.  
  
**메타 데이터를 찾아보려면**  
  
1.  액세스 메타 데이터 탐색기에서 **액세스-메타 베이스**를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
2.  검토할 데이터베이스를 확장 한 다음 **쿼리**를 확장 합니다.  
  
    쿼리 목록을 확인 합니다. 쿼리를 선택 하면 오른쪽 창에 **SQL** 탭과 **속성** 탭이 나타납니다.  
  
3.  **테이블** 을 확장 한 다음 테이블을 선택 합니다.  
  
    **테이블**, **형식 매핑**, **속성**및 **데이터**라는 4 개의 탭이 표시 됩니다.  
  
4.  테이블을 확장 하 고 **키**를 확장 한 다음 키를 선택 합니다.  
  
    키 속성이 오른쪽 창에 표시 됩니다.  
  
5.  **인덱스**를 확장 한 다음 인덱스를 선택 합니다.  
  
    오른쪽 창에 인덱스 속성이 표시 됩니다.  
  
## <a name="refreshing-databases"></a>데이터베이스 새로 고침  
파일을 추가한 후에 Access 데이터베이스를 변경 하는 경우 Access 데이터베이스에서 메타 데이터를 업데이트할 수 있습니다.  
  
**액세스 메타 데이터를 업데이트 하려면**  
  
-   액세스 메타 데이터 탐색기에서 데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 새로 고침**을 선택 합니다.  
  
## <a name="removing-databases"></a>데이터베이스 제거  
다음 단계를 수행 하 여 프로젝트에서 Access 데이터베이스를 제거할 수 있습니다.  
  
**프로젝트에서 데이터베이스를 제거 하려면**  
  
1.  액세스 메타 데이터 탐색기에서 **액세스-메타 베이스**를 확장 한 다음 **데이터베이스**를 확장 합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스 제거**를 선택 합니다.  
  
## <a name="next-step"></a>다음 단계  
마이그레이션 프로세스의 다음 단계는 [SQL Server에 연결](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)하는 것입니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[프로젝트 만들기 및 관리](creating-and-managing-projects-accesstosql.md)  
  
