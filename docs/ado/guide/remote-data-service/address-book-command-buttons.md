---
title: "주소록 명령 단추 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 31b0bb389b188c39b4590a774ac453a9de17fd56
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="address-book-command-buttons"></a>주소록 명령 단추
주소록 응용 프로그램에 다음과 같은 명령 단추가 포함 됩니다.  
  
-   A **찾을** 알림 데이터베이스에 쿼리를 제출 단추입니다.  
  
-   A **지우기** 단추를 새 검색을 시작 하기 전에 텍스트 상자의 선택을 취소 합니다.  
  
-   **프로필 업데이트** 직원 레코드에 변경 사항을 저장 합니다.  
  
-   A **변경 내용 취소** 변경 내용을 취소 하는 단추입니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="find-button"></a>찾기 단추  
 클릭 하 고 **찾을** 빌드되고 SQL 쿼리를 전송 하는 VBScript Find_OnClick Sub 프로시저를 활성화 하는 단추입니다. 이 단추를 클릭 하면 데이터 표를 채웁니다.  
  
## <a name="building-the-sql-query"></a>SQL 쿼리 작성  
 Find_OnClick Sub 프로시저의 첫 번째 부분을 글로벌 SQL SELECT 문에 텍스트 문자열을 추가 하 여 SQL 쿼리를 한 번에 하나의 구 작성 합니다. 변수를 설정 하 여 시작할 `myQuery` 데이터 원본 테이블에서 모든 데이터 행을 요청 하는 SQL SELECT 문과 합니다. 다음으로, Sub 프로시저 검사 각 페이지에서 4 개의 입력된 상자를 사용 합니다.  
  
 프로그램은 단어를 사용 하기 때문에 `like` SQL 문을 작성 데, 쿼리는 정확히 일치 하지 않고 부분 문자열을 검색 합니다.  
  
 예를 들어 경우는 **성** 상자 "Berge" 항목을 추가할 및 **제목** 상자 SQL 문 "프로그램 관리자" 항목을 추가할 (값 `myQuery`) 조건인:  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 쿼리가 성공 하면 프로그램 "Manager" (예: 프로그램 관리자, 고급 기술) 단어를 포함 하는 제목 및 "Berge" (예: Berge 및 Berger) 텍스트를 포함 하는 성을 가진 모든 사람이 HTML 데이터 표에 표시 됩니다.  
  
## <a name="preparing-and-sending-the-query"></a>준비 및 쿼리 보내기  
 Find_OnClick Sub 프로시저의 마지막 부분 두 개의 문으로 구성 됩니다. 첫 번째 문에서 할당 된 [SQL](../../../ado/reference/rds-api/sql-property.md) 속성은 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체와 같은 동적으로 작성 된 SQL 쿼리 합니다. 두 번째 문을 사용 하면는 **.rds입니다 DataControl** 개체 (`DC1`) 데이터베이스를 쿼리하고 다음 표에 쿼리의 새 결과 표시 합니다.  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>프로필 업데이트 단추  
 클릭 하 고 **프로필 업데이트** 를 실행 하는 VBScript Update_OnClick Sub 프로시저를 활성화 하는 단추는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 및 [새로 고침](../../../ado/reference/rds-api/refresh-method-rds.md) 메서드.  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 때 `DC1.SubmitChanges` 실행 되 면 원격 데이터 서비스 업데이트 정보를 모든 패키지 및 HTTP 통해 서버에 보냅니다. 업데이트는 전부 아니면 전무; 업데이트의 일부로 실패할 경우 이루어집니다 변경 하 고 상태 메시지가 반환 됩니다. `DC1.Refresh`후 작업이 필요 하지 않습니다 **SubmitChanges** 원격 데이터 서비스와 있지만 새로운 데이터를 확인 합니다.  
  
## <a name="cancel-changes-button"></a>변경 내용 취소 단추  
 클릭 하면 **변경 내용 취소** 를 실행 하는 VBScript Cancel_OnClick Sub 프로시저를 활성화 하는 [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체의 (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) 메서드.  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 때 `DC1.CancelUpdate` 를 실행 하면 마지막 쿼리 또는 업데이트 이후 데이터 표에 직원 레코드에 사용자가 변경한 모든 편집 합니다. 원래 값을 복원 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [주소록 탐색 단추](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)



