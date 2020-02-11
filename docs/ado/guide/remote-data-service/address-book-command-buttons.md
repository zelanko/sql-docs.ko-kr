---
title: 주소록 명령 단추 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d1aa5b628bec9399374b94a2cd78090207bf09b7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922981"
---
# <a name="address-book-command-buttons"></a>주소록 명령 단추
주소록 응용 프로그램에는 다음 명령 단추가 포함 됩니다.  
  
-   데이터베이스에 쿼리를 제출 하는 **찾기** 단추  
  
-   새 검색을 시작 하기 전에 텍스트 상자를 지우는 **clear** 단추입니다.  
  
-   직원 레코드에 대 한 변경 내용을 저장 하는 **프로필 업데이트** 단추  
  
-   변경 **내용 취소 단추를** 클릭 하면 변경 내용이 취소 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="find-button"></a>찾기 단추  
 [ **찾기** ] 단추를 클릭 하면 SQL 쿼리를 작성 하 고 전송 하는 VBScript Find_OnClick Sub 프로시저가 활성화 됩니다. 이 단추를 클릭 하면 데이터 표가 채워집니다.  
  
## <a name="building-the-sql-query"></a>SQL 쿼리 작성  
 Find_OnClick Sub 프로시저의 첫 번째 부분에서는 텍스트 문자열을 전역 SQL SELECT 문에 추가 하 여 SQL 쿼리를 한 번에 하나씩 작성 합니다. 먼저 데이터 원본 테이블의 모든 `myQuery` 데이터 행을 요청 하는 SQL SELECT 문으로 변수를 설정 합니다. 그런 다음 하위 프로시저는 페이지에서 4 개의 입력 상자를 각각 검색 합니다.  
  
 프로그램은 SQL 문을 작성 하 `like` 는 데 사용 되는 단어를 사용 하기 때문에 쿼리는 정확히 일치 하는 항목이 아닌 부분 문자열 검색입니다.  
  
 예를 들어 **Last Name** 상자에 "trge" 항목이 포함 되어 있고 **제목** 상자에 "Program Manager" 항목이 포함 된 경우 SQL 문 (값 `myQuery`)은 다음을 읽습니다.  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 쿼리가 정상적으로 실행 되 면 "Berger Ge" (예:) 라는 텍스트와 "Program Manager" (예: 프로그램 관리자, 고급 기술) 라는 단어가 포함 된 제목이 있는 모든 사람이 HTML 데이터 표에 표시 됩니다.  
  
## <a name="preparing-and-sending-the-query"></a>쿼리 준비 및 보내기  
 Find_OnClick Sub 프로시저의 마지막 부분은 두 개의 문으로 구성 됩니다. 첫 번째 문은 RDS의 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성을 할당 합니다 [. ](../../../ado/reference/rds-api/datacontrol-object-rds.md)동적으로 작성 된 SQL 쿼리와 같은 DataControl 개체입니다. 두 번째 문은 RDS를 발생 시킵니다 **. **데이터베이스를 쿼리`DC1`한 다음 쿼리의 새 결과를 표에 표시 하는 DataControl 개체 ()입니다.  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>프로필 업데이트 단추  
 **프로필 업데이트** 단추를 클릭 하면 VBScript Update_OnClick Sub 프로시저를 활성화 하 여 RDS를 실행 합니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 및 [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md) 메서드  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 가 `DC1.SubmitChanges` 실행 되 면 원격 데이터 서비스에서 모든 업데이트 정보를 패키지 하 여 HTTP를 통해 서버에 보냅니다. 업데이트는 모두 또는 없음입니다. 업데이트의 일부가 실패 하면 변경 내용이 적용 되지 않고 상태 메시지가 반환 됩니다. `DC1.Refresh`는 원격 데이터 서비스를 **SubmitChanges** 한 후에는 필요 하지 않지만 새로운 데이터를 보장 합니다.  
  
## <a name="cancel-changes-button"></a>변경 내용 취소 단추  
 **변경 내용 취소** 를 클릭 하면 VBScript Cancel_OnClick Sub 프로시저가 활성화 되어 RDS를 실행 합니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) 메서드.  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 가 `DC1.CancelUpdate` 실행 되 면 마지막 쿼리 또는 업데이트 이후 데이터 표에서 직원 레코드에 대해 수행한 모든 편집 내용이 삭제 됩니다. 원래 값을 복원 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [주소록 탐색 단추](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


