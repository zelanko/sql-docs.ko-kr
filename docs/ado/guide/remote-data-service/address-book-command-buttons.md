---
title: 주소록 명령 단추 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64570b9a6f2052fdc3f9e5544a442853110587b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47613151"
---
# <a name="address-book-command-buttons"></a>주소록 명령 단추
주소록 응용 프로그램에는 다음과 같은 명령 단추가 포함:  
  
-   A **찾을** 데이터베이스 쿼리를 제출 하는 단추입니다.  
  
-   A **의 선택을 취소** 단추를 새 검색을 시작 하기 전에 입력란의 선택을 취소 합니다.  
  
-   **프로필 업데이트** 직원 레코드에 변경 사항을 저장 합니다.  
  
-   A **변경 내용을 취소** 변경 내용을 취소 하는 단추입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="find-button"></a>찾기 단추  
 클릭 하는 **찾을** 단추가 활성화 VBScript Find_OnClick 하위 프로시저를 작성 하 고 SQL 쿼리를 보냅니다. 이 단추를 클릭 하면 데이터 그리드를 채웁니다.  
  
## <a name="building-the-sql-query"></a>SQL 쿼리 작성  
 Find_OnClick Sub 프로시저의 첫 번째 부분을 전역 SQL SELECT 문에 텍스트 문자열을 추가 하 여 SQL 쿼리를 한 번에 하나의 구를 빌드합니다. 변수를 설정 하 여 시작할 `myQuery` 데이터 원본 테이블에서 모든 데이터 행을 요청 하는 SQL SELECT 문으로 합니다. 다음으로, Sub 프로시저를 각 페이지의 네 가지 입력된 상자 검색합니다.  
  
 프로그램 단어를 사용 하므로 `like` SQL 문을 작성, 쿼리는 정확히 일치 하는 것이 아니라 하위 문자열을 검색 합니다.  
  
 예를 들어 경우는 **Last Name** 상자에 "Berge" 항목을 포함 및 **제목** 상자 항목 "프로그램 관리자," SQL 문이 포함 된 (값 `myQuery`)를 읽는:  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 쿼리가 성공 하면 "프로그램 관리자" (예: 프로그램 관리자, 고급 기술) 단어가 포함 된 제목을 텍스트 "Berge" (예: Berge 및 Berger)를 포함 하는 성을 가진 모든 사람 HTML 데이터 표에 표시 됩니다.  
  
## <a name="preparing-and-sending-the-query"></a>쿼리를 보내고 준비  
 Find_OnClick Sub 프로시저의 마지막 부분은 두 개의 문으로 구성 됩니다. 첫 번째 문은 할당 합니다 [SQL](../../../ado/reference/rds-api/sql-property.md) 의 속성을 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체를 동적으로 작성 된 SQL 쿼리 합니다. 두 번째 문은 **rds. DataControl** 개체 (`DC1`)를 데이터베이스에 쿼리하고 다음 표의 새 쿼리 결과 표시 합니다.  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>프로필 [업데이트] 단추  
 클릭 하는 **프로필 업데이트** 실행 하는 VBScript Update_OnClick 하위 프로시저를 활성화 하는 단추는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 하 고 [새로 고침](../../../ado/reference/rds-api/refresh-method-rds.md) 메서드.  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 때 `DC1.SubmitChanges` 실행, 원격 데이터 서비스 업데이트 정보를 모든 패키지 및 HTTP 통해 서버에 보냅니다. 이 업데이트는 이것 아니면 저것 인; 업데이트의 일부 실패할 경우 변경 됩니다 하 고 상태 메시지가 반환 됩니다. `DC1.Refresh` 후 필요 하지 않습니다 **SubmitChanges** 원격 데이터 서비스를 사용 하 여 새로운 데이터 보장 하지만 합니다.  
  
## <a name="cancel-changes-button"></a>변경 내용 취소 단추  
 클릭 **변경 내용을 취소** 실행 하는 VBScript Cancel_OnClick 하위 프로시저를 활성화 합니다 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) 메서드.  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 때 `DC1.CancelUpdate` 실행 마지막 쿼리 또는 업데이트 이후 사용자가 데이터 표에서 직원 레코드에 수행한 모든 편집 내용을 삭제 합니다. 원래 값을 복원합니다.  
  
## <a name="see-also"></a>관련 항목  
 [주소록 탐색 단추](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


