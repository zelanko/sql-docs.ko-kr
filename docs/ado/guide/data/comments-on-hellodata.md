---
title: HelloData에 대 한 설명 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c4897f82ff8562c031ec3522f47cddebfb56eb2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925803"
---
# <a name="comments-on-hellodata"></a>HelloData에 대한 설명
HelloData 응용 프로그램은 일반적인 ADO 응용 프로그램의 기본 작업 (데이터 가져오기, 검사, 편집 및 업데이트)을 단계별로 안내 합니다. 응용 프로그램을 시작할 때 첫 번째 단추인 **데이터 가져오기**를 클릭 합니다. 이렇게 하면 **GetData** 서브루틴이 실행 됩니다.  
  
## <a name="getdata"></a>GetData  
 **GetData** 는 올바른 연결 문자열을 모듈 수준 변수 *m_sConnStr*에 배치 합니다. 연결 문자열에 대 한 자세한 내용은 [연결 문자열 만들기](../../../ado/guide/data/creating-a-connection-string.md)를 참조 하세요.  
  
 Visual Basic **OnError** 문을 사용 하 여 오류 처리기를 할당 합니다. ADO의 오류 처리에 대 한 자세한 내용은 [오류 처리](../../../ado/guide/data/error-handling.md)를 참조 하세요. HelloData 예제에서 *연결이 끊어진 레코드 집합*을 만들기 때문에 새 **연결** 개체가 만들어지고 **CursorLocation** 속성은 **adUseClient** 로 설정 됩니다. 즉, 데이터 원본에서 데이터를 가져온 후 데이터 원본에 대 한 실제 연결이 끊어지고 **레코드 집합** 개체에서 로컬로 캐시 된 데이터를 계속 사용할 수 있습니다.  
  
 연결을 연 후 변수에 SQL 문자열을 할당 합니다 (sSQL). 그런 다음 새 **레코드 집합** 개체의 인스턴스를 `m_oRecordset1`만듭니다. 다음 코드 줄에서 기존 **연결**을 통해 **레코드 집합** 을 열고를 **레코드 집합**의 원본 `sSQL` 으로 전달 합니다. **레코드 집합** 의 원본으로 전달 된 SQL 문자열을 확인 하는 데 도움이 되는 ADO는 최종 인수의 **Adcmdtext** 를 **recordset Open** 메서드에 전달 하 여 명령의 텍스트 정의입니다. 이 줄에는 **레코드 집합과**연결 된 **LockType** 및 **CursorType** 설정 됩니다.  
  
 코드의 다음 줄에서는 **MarshalOptions** 속성을 **adMarshalModifiedOnly**로 설정 합니다. **MarshalOptions** 는 중간 계층 (또는 웹 서버)으로 마샬링되는 레코드를 나타냅니다. 마샬링에 대 한 자세한 내용은 COM 설명서를 참조 하십시오. 클라이언트 쪽 커서 ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)와 함께 **adMarshalModifiedOnly** 를 사용 하는 경우 클라이언트에서 수정 된 레코드만 중간 계층에 다시 기록 됩니다. **MarshalOptions** 를 **adMarshalModifiedOnly** 로 설정 하면 마샬링되는 행이 줄어들기 때문에 성능을 향상 시킬 수 있습니다.  
  
 그런 다음 **ActiveConnection** 속성을 **Nothing**으로 설정 하 여 **레코드 집합** 의 연결을 끊습니다. 자세한 내용은 [데이터 업데이트 및 유지](../../../ado/guide/data/updating-and-persisting-data.md)에서 "레코드 집합 연결 끊기 및 다시 연결" 섹션을 참조 하세요.  
  
 데이터 원본에 대 한 연결을 닫고 기존 **연결** 개체를 삭제 합니다. 그러면 사용 된 리소스가 해제 됩니다.  
  
 최종 단계는 폼에서 **레코드 집합** 의 데이터를 쉽게 표시할 수 있도록 **레코드** 집합을 Microsoft DataGrid 컨트롤의 데이터 **원본** 으로 설정 하는 것입니다.  
  
 두 번째 단추를 클릭 하 여 **데이터를 검사**합니다. 그러면 **ExamineData** 서브루틴이 실행 됩니다.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData는 **레코드** 집합 개체의 다양 한 메서드 및 속성을 사용 하 여 **레코드 집합**의 데이터에 대 한 정보를 표시 합니다. **RecordCount** 속성을 사용 하 여 레코드 수를 보고 합니다. **레코드 집합** 을 반복 하 고 폼의 표시 텍스트 상자에 **AbsolutePosition** 속성 값을 출력 합니다. 또한 루프에서 세 번째 레코드의 **Bookmark** 속성 값은 나중에 사용 하기 위해 변형 변수 *vbookmark*에 배치 됩니다.  
  
 루틴은 이전에 저장 된 책갈피 변수를 사용 하 여 세 번째 레코드로 직접 이동 합니다. 루틴은 **WalkFields** 서브루틴을 호출 하 여 **레코드 집합** 의 **Fields** 컬렉션을 반복 하 고 컬렉션의 각 **필드** 에 대 한 세부 정보를 표시 합니다.  
  
 마지막으로 **ExamineData** 는 **레코드 집합** 의 **필터** 속성을 사용 하 여 **CategoryId** 가 2 인 레코드만을 화면에 포함 합니다. 이 필터를 적용 한 결과는 폼의 표시 표에 즉시 표시 됩니다.  
  
 **ExamineData** 서브루틴에 표시 되는 기능에 대 한 자세한 내용은 [데이터 검사](../../../ado/guide/data/examining-data.md)를 참조 하십시오.  
  
 그런 다음 세 번째 단추인 **데이터 편집**을 클릭 합니다. 그러면 **Editdata** 서브루틴이 실행 됩니다.  
  
## <a name="editdata"></a>EditData  
 코드가 **Editdata** 서브루틴에 들어가면 **레코드 집합** 은 필터 조건을 충족 하는 항목만 표시 되도록 **CategoryId** 에서 2로 계속 필터링 됩니다. 먼저 **레코드 집합** 을 반복 하 고 **레코드 집합** 에서 표시 되는 각 항목의 가격을 10% 늘립니다. **Price** 필드의 값은 해당 필드의 **value** 속성을 유효한 새 양과 동일 하 게 설정 하 여 변경 됩니다.  
  
 **레코드 집합** 은 데이터 원본에서 연결이 끊어집니다. **Editdata** 에서 변경한 내용은 데이터의 로컬로 캐시 된 복사본에만 적용 됩니다. 자세한 내용은 [데이터 편집](../../../ado/guide/data/editing-data.md)을 참조 하세요.  
  
 네 번째 단추인 **데이터 업데이트**를 클릭 하기 전에는 데이터 원본에 대 한 변경 내용이 적용 되지 않습니다. 이렇게 하면 **Updatedata** 서브루틴이 실행 됩니다.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData는 먼저 **레코드 집합**에 적용 된 필터를 제거 합니다. 이 코드는 필터링 되지 `m_oRecordset1` 않은 **레코드 집합이** 모눈에 표시 되도록 폼에서 Microsoft 바인딩된 DataGrid의 **데이터 원본** 으로을 제거 하 고 다시 설정 합니다.  
  
 그런 다음 **adMovePrevious** 인수를 사용 하 여 **지원** 메서드를 사용 하 여 **레코드 집합** 에서 뒤로 이동할 수 있는지 여부를 확인 합니다.  
  
 루틴은 **MoveFirst** 메서드를 사용 하 여 첫 번째 레코드로 이동 하 고 **Field** 개체의 **originalvalue** 및 **Value** 속성을 사용 하 여 필드의 원래 값과 현재 값을 표시 합니다. 이러한 속성은 **UnderlyingValue** 속성 (여기서는 사용 되지 않음)과 함께 [데이터 업데이트 및 유지](../../../ado/guide/data/updating-and-persisting-data.md)에 설명 되어 있습니다.  
  
 그런 다음 새 **연결** 개체를 만들고 사용 하 여 데이터 원본에 대 한 연결을 다시 설정 합니다. 레코드 집합에 대 한 **ActiveConnection** 으로 새 **연결** 을 설정 하 여 **레코드 집합** 을 데이터 원본에 다시 연결 **합니다.** 서버에 업데이트를 보내기 위해 코드는 **레코드 집합**에서 **UpdateBatch** 를 호출 합니다.  
  
 일괄 업데이트가 성공 하면 모듈 수준 플래그 변수 `m_flgPriceUpdated`가 True로 설정 됩니다. 그러면 나중에 데이터베이스에 대해 수행 된 모든 변경 내용을 정리 하는 알림이 표시 됩니다.  
  
 마지막으로, 코드는 **레코드 집합** 의 첫 번째 레코드로 다시 이동 하 고 원래 값과 현재 값을 표시 합니다. 값은 **UpdateBatch**를 호출한 후에 동일 합니다.  
  
 데이터를 업데이트 하는 방법에 대 한 자세한 내용은 **레코드 집합** 의 연결이 끊어질 때 서버의 데이터가 변경 될 때 수행할 작업을 비롯 하 여 데이터 업데이트 [및 유지](../../../ado/guide/data/updating-and-persisting-data.md)를 참조 하세요.  
  
## <a name="form_unload"></a>Form_Unload  
 **Form_Unload** 서브루틴은 여러 가지 이유로 중요 합니다. 첫째,이 응용 프로그램은 응용 프로그램을 종료 하기 전에 데이터베이스에 적용 된 변경 내용을 정리 하는 Form_Unload. 둘째, 코드는 **Execute** 메서드를 사용 하 여 열린 **연결** 개체에서 직접 명령을 실행할 수 있는 방법을 보여 줍니다. 마지막으로 데이터 원본에 대해 행을 반환 하지 않는 쿼리 (업데이트 쿼리)를 실행 하는 예를 보여 줍니다.
