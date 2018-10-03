---
title: Access 인벤토리 (AccessToSQL) 내보내기 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f35ae03cb6588bc7828349dd4a4beafcc5a7b2f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746451"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Access 인벤토리 (AccessToSQL) 내보내기
Access 데이터베이스를 여러 개 있고 깨달음을로 마이그레이션하려면 확실 하지 않은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 프로젝트의 모든 Access 데이터베이스의 인벤토리를 내보낼 수 있습니다. 검토 하 고 데이터베이스 및 마이그레이션하려면 해당 데이터베이스 내의 개체가 결정 인벤토리 메타 데이터를 쿼리할 수 있습니다. 이 인벤토리 사용 하면 신속 하 게 다음과 같은 질문에 답변 찾기:  
  
-   큰 데이터베이스의 경우 이란?  
  
-   대부분의 데이터베이스 소유자?  
  
-   데이터베이스 테이블에 동일한 테이블에 포함?  
  
-   데이터베이스를 지난 6 개월 동안에서 수정 되지 않은?  
  
-   데이터베이스에 개인 정보가 있습니까?  
  
이러한 질문에 대답 하는 데 사용 되는 쿼리 예제는이 항목의 끝에서 제공 됩니다.  
  
## <a name="exported-metadata"></a>내보낸된 메타 데이터  
SSMA는 Access 데이터베이스, 테이블, 열, 인덱스, 외래 키, 쿼리, 보고서, forms, 매크로 및 모듈에 대 한 메타 데이터를 내보냅니다. 각 항목의 이러한 범주에 대 한 메타 데이터를 별도 테이블에 내보냅니다. 이러한 테이블의 스키마를 참조 하세요 [Access 인벤토리 스키마](access-inventory-schemas-accesstosql.md)합니다.  
  
## <a name="exporting-inventory-data"></a>인벤토리 데이터 내보내기  
Access 인벤토리 내보내기 있습니다 먼저 또는 SSMA 프로젝트를 만듭니다 열고 분석 하려는 Access 데이터베이스를 추가 합니다. 지정 된 해당 데이터베이스에 대 한 메타 데이터를 내보낼 SSMA 프로젝트에 데이터베이스를 추가한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 및 스키마입니다. 필요한 경우 SSMA 메타 데이터를 저장 하는 테이블을 만듭니다. SSMA는 Access 데이터베이스에 대 한 메타 데이터 추가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.  
  
> [!NOTE]  
> Access 데이터베이스를 여러 파일로 분할할 수 있습니다: 테이블 및 쿼리, 폼, 보고서, 매크로, 모듈 및 바로 가기 키를 포함 하는 프런트 엔드 데이터베이스를 포함 하는 백 엔드 데이터베이스입니다. 분할 데이터베이스를 마이그레이션할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA에 프런트 엔드 데이터베이스를 추가 합니다.  
  
다음 지침 프로젝트 만들기, 프로젝트에 데이터베이스 추가, 연결 하는 방법에 설명 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 인벤토리 데이터를 저장 하십시오.  
  
**프로젝트를 만들려면**  
  
1.  Access 용 SSMA를 엽니다.  
  
2.  **파일** 메뉴에서 **새 프로젝트**를 선택합니다.  
  
    **새 프로젝트** 대화 상자가 나타납니다.  
  
3.  **이름** 입력란에 프로젝트 이름을  
  
4.  에 **위치** 상자에 입력 하거나 프로젝트에 대 한 폴더를 선택 합니다.  
  
5.  에 **마이그레이션** 콤보 상자를 마이그레이션하고, 클릭 하려는 대상 버전을 선택 합니다 **확인**합니다.  
  
프로젝트를 만드는 방법에 대 한 자세한 내용은 참조 하세요. [Creating and Managing Projects](creating-and-managing-projects-accesstosql.md)합니다.  
  
**찾아 데이터베이스를 추가 합니다.**  
  
1.  에 **파일** 메뉴에서 클릭 **찾을 데이터베이스**합니다.  
  
2.  데이터베이스 찾기 마법사에서 드라이브, 파일 경로 또는 UNC 경로 검색 하려면를 입력 합니다. 를 클릭할 **찾아보기** 드라이브 또는 네트워크 폴더를 선택 합니다.  
  
3.  클릭 **추가** 목록 상자에 위치를 추가 합니다.  
  
    추가 검색 위치를 추가 하려면 이전 두 단계를 반복 합니다.  
  
4.  필요에 따라 반환 되는 데이터베이스의 목록을 구체화 하려면 검색 조건을 추가 합니다.  
  
    > [!IMPORTANT]  
    > 합니다 **파일 이름의 일부나 전부** 입력란 와일드 카드 문자를 지원 하지 않습니다.  
  
5.  클릭 **스캔**합니다.  
  
    검색 페이지가 표시 됩니다. 검색 된 데이터베이스 및 검색 진행률을 보여 줍니다. 검색을 중지 하려면 클릭 **중지**합니다.  
  
6.  파일 선택 페이지에서 프로젝트에 추가 하려는 각 데이터베이스를 선택 합니다.  
  
    사용할 수는 **모두 선택** 하 고 **모두 지우기** 선택 하거나 모든 데이터베이스를 선택 취소 목록의 맨 위에 있는 단추입니다. 여러 행을 선택 하려면 CTRL 키를 누른 채로 또는 SHIFT 키를 선택 범위의 행을 아래로 수도 있습니다.  
  
7.  **다음**을 클릭합니다.  
  
8.  확인 페이지에서 클릭 **완료**합니다.  
  
데이터베이스 프로젝트를 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [Access 데이터베이스 파일 제거 및 추가](adding-and-removing-access-database-files-accesstosql.md)합니다.  
  
**SQL Server에 연결 하려면**  
  
1.  에 **파일** 메뉴에서 **SQL Server에 연결**합니다.  
  
2.  연결 대화 상자에서 이름을 입력 하거나 선택 된 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
    -   로컬 컴퓨터의 기본 인스턴스에 연결 하는 경우 입력할 수 있습니다 **localhost** 또는 점 (**.**).  
  
    -   다른 컴퓨터의 기본 인스턴스에 연결 하는 경우에 컴퓨터의 이름을 입력 합니다.  
  
    -   명명 된 인스턴스에 연결 하는 경우 컴퓨터 이름, 백슬래시 및 인스턴스 이름을 입력 합니다. 예를 들어: MyServer\MyInstance 합니다.  
  
3.  에 **데이터베이스** 상자에서 내보낸된 메타 데이터에 대 한 대상 데이터베이스의 이름을 입력 합니다.  
  
4.  경우 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 사용 되는 포트 번호를 입력, 기본이 아닌 포트에서 연결을 허용 하도록 구성 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결 합니다 **서버 포트** 상자입니다. 기본 인스턴스에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 기본 포트 번호는 1433입니다. 명명 된 인스턴스의 경우 SSMA에서 포트 번호 가져오기를 시도 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스입니다.  
  
5.  에 **인증** 드롭 다운 메뉴에서 연결에 사용할 인증 유형입니다. 현재 Windows 계정을 사용 하려면 선택 **Windows 인증**합니다. 사용 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 선택 **SQL Server 인증**, 사용자 이름 및 암호를 제공 합니다.  
  
연결에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server에 연결 &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md)합니다.  
  
**인벤토리 정보를 내보내려면**  
  
1.  액세스 메타 데이터 탐색기에서 확장 **액세스-메타 베이스**합니다.  
  
2.  옆에 확인란을 선택 **데이터베이스**합니다.  
  
    개별 데이터베이스 또는 데이터베이스 개체를 생략 하려면 확장 합니다 **데이터베이스** 폴더 및 데이터베이스 또는 데이터베이스 개체 옆의 확인란의 선택을 취소 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **데이터베이스** 선택한 **스키마 내보내기**합니다.  
  
4.  에 **내보내기에 대 한 스키마 선택** 대화 상자에서 내보낸된 메타 데이터에 대 한 대상 스키마를 선택한 다음 클릭 **확인**합니다.  
  
메타 데이터를 내보낼 때마다 SSMA 인벤토리 데이터를 추가 합니다. 인벤토리의 기존 데이터를 업데이트 하거나 삭제 합니다.  
  
## <a name="querying-the-exported-metadata"></a>내보낸된 메타 데이터를 쿼리합니다.  
Access 데이터베이스에 대 한 메타 데이터를 내보낸 후에 메타 데이터를 쿼리할 수 있습니다. 다음 지침에 쿼리 편집기 창을 사용 하 여 설명 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리를 실행할 수 있습니다.  
  
**쿼리 메타 데이터**  
  
1.  **시작** 메뉴에서 **모든 프로그램**를 가리키고 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** 또는 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008**나 **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**를 클릭 하 고 **SQL Server Management Studio**합니다.  
  
2.  에 **서버에 연결** 대화 상자에서 설정을 확인 하 고 클릭 **Connect**합니다.  
  
3.  Management Studio 도구 모음에서 클릭 **새 쿼리** 쿼리 편집기를 엽니다.  
  
4.  쿼리 편집기 창에서 쿼리를 입력 합니다. 몇 가지 예는 다음 섹션에 표시 됩니다.  
  
5.  쿼리를 실행 하려면 F5 키를 누릅니다.  
  
## <a name="query-examples"></a>쿼리 예제  
사용 하 여 다음 쿼리를 실행 하기 전에 실행할지 *database_name* 쿼리 내보낸된 메타 데이터를 포함 하는 데이터베이스에 대해 실행 되 고 있는지 확인 하는 쿼리. 예를 들어 MyAccessMetadata 라는 데이터베이스에 메타 데이터를 내보낸 경우 추가할 때 다음 부분에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드:  
  
```  
USE MyAccessMetadata;  
GO  
```  
다음 예에서는 모두 사용 합니다 **dbo** 스키마입니다. 다른 스키마에 메타 데이터를 내보낸 경우 이러한 쿼리를 실행할 때 스키마를 변경 해야 합니다.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>이러한 데이터베이스에서 테이블 및 열?  
다음 쿼리는 열, 테이블 및 데이터베이스 메타 데이터를 포함 하는 테이블을 조인 하 고 모든 데이터베이스, 테이블 및 열 이름을 기준으로 정렬 하는 열 이름을 반환 합니다.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>큰 데이터베이스의 경우 이란?  
다음 쿼리 파일 크기 별로 정렬 된 각 Access 데이터베이스에서 데이터베이스 이름, 파일 크기 및 개수 테이블을 반환 합니다.  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>대부분의 데이터베이스 소유자는 누구 인가요?  
다음 쿼리는 데이터베이스 이름과 소유자에 의해 정렬 된 각 Access 데이터베이스의 소유자를 반환 합니다.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>데이터베이스 테이블에 동일한 테이블에 포함?  
다음 쿼리는 테이블, 목록에 두 번 이상 나타나는 모든 테이블 이름을 찾으려면 하위 쿼리를 사용 하 고 테이블에이 목록을 사용 하 여 데이터베이스 이름을 가져오려면. 결과 데이터베이스 이름을 차례로 테이블 이름으로 반환 되 고 테이블 이름으로 정렬 됩니다.  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>데이터베이스를 지난 6 개월 동안 수정 되지 않은?  
다음 쿼리는 현재 날짜를 가져옵니다, 그리고 전, 6 개월 동안 월 값을 가져옵니다 및 다음 6 개월 보다 큰 수정 된 날짜를 사용 하 여 데이터베이스의 목록을 반환 합니다.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>데이터베이스에 개인 정보가 있습니까?  
Access 데이터베이스는 중요 한 정보나 개인 정보를 포함할 수 있습니다. 이러한 데이터베이스를 이동 하려는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 보안 기능을 활용할 수 있습니다. 중요 한 데이터가 포함 된 열 특정 이름, 또는를 특정 문자를 포함 하는 경우에 해당 정보를 포함 하는 모든 열을 찾으려면 쿼리를 사용할 수 있습니다. 예를 들어, "급여" 문자열이 포함 된 모든 열을 찾을 수 있습니다.  쿼리는 다음 데이터베이스 이름, 테이블 이름과 열 이름을 반환합니다.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
열 이름을 모르는 경우에 모든 열을 반환 하는 쿼리를 작성할 수 있습니다. 이렇게 하려면 이전 쿼리에서 WHERE 절을 제거 합니다.  
  
## <a name="see-also"></a>관련 항목  
[Access 데이터베이스 마이그레이션 준비](preparing-access-databases-for-migration-accesstosql.md)  
  
