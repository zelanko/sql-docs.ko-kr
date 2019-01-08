---
title: HelloData에 | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 632703a1f7817986a6bc192006ef079af20cfb08
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527451"
---
# <a name="comments-on-hellodata"></a>HelloData에 대한 설명
HelloData 응용 프로그램을 일반적인 ADO 응용 프로그램의 기본 작업을 통해 단계: 가져오기, 검사, 편집 및 데이터를 업데이트 합니다. 응용 프로그램을 시작 하면 첫 번째 단추를 클릭 **데이터 가져오기**합니다. 이렇게 하면 실행 합니다 **GetData** 서브루틴입니다.  
  
## <a name="getdata"></a>GetData  
 **GetData** 모듈 수준 변수를에 유효한 연결 문자열을 붙여 넣습니다 *m_sConnStr*합니다. 연결 문자열에 대 한 자세한 내용은 참조 하세요. [연결 문자열 만들기](../../../ado/guide/data/creating-a-connection-string.md)합니다.  
  
 Visual Basic을 사용 하 여 오류 처리기를 할당 **OnError** 문입니다. Ado에서 오류 처리에 대 한 자세한 내용은 참조 하세요. [오류 처리](../../../ado/guide/data/error-handling.md)합니다. 새 **연결** 개체를 만든 하며 **CursorLocation** 속성이로 설정 되어 **adUseClient** HelloData 예제 만들기 때문에  *연결이 끊긴 레코드 집합*합니다. 즉, 데이터 원본에서 데이터를 가져온, 데이터 소스를 사용 하 여 물리적 연결이 끊어지지만 로컬로 캐시 되는 데이터를 사용 하 여 계속 작업할 수 있습니다는 즉시 사용자 **레코드 집합** 개체입니다.  
  
 연결이 열린 후 변수에 (sSQL)는 SQL 문자열을 할당 합니다. 다음의 새 인스턴스를 만듭니다 **Recordset** 개체를 `m_oRecordset1`입니다. 코드의 다음 줄에서 엽니다는 **레코드 집합** 기존 **연결**전달 `sSQL` 원본으로는 **레코드 집합**합니다. ADO SQL 문자열을 결정 되도록 할 수의 원본으로 전달한를 **레코드 집합** 전달 하 여는 명령 텍스트 정의 **adCmdText** 마지막 인수에 **레코드 집합 열기** 메서드. 이 줄도 설정 합니다 **LockType** 및 **CursorType** 연관를 **레코드 집합**합니다.  
  
 코드 집합의 다음 줄을 **MarshalOptions** 속성이 **adMarshalModifiedOnly**합니다. **MarshalOptions** 레코드를 중간 계층 (또는 웹 서버)로 마샬링되어야를 나타냅니다. 마샬링에 대 한 자세한 내용은 COM 설명서를 참조 하십시오. 사용 하는 경우 **adMarshalModifiedOnly** 클라이언트 쪽 커서를 사용 하 여 ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)에서 수정 된 레코드만 클라이언트는 중간 계층에 다시 기록 됩니다. 설정 **MarshalOptions** 하 **adMarshalModifiedOnly** 마샬링되는 적은 수의 행 때문에 성능을 향상 시킬 수 있습니다.  
  
 다음으로, 연결 끊기 합니다 **레코드 집합** 설정 하 여 해당 **ActiveConnection** 속성이 **Nothing**합니다. 자세한 내용은 "연결 끊기 및 다시 연결 하는 레코드 집합" 섹션을 참조 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.  
  
 데이터 원본에 대 한 연결을 닫고 기존 파괴 **연결** 개체입니다. 이 사용 되는 리소스를 해제 합니다.  
  
 최종 단계는 합니다 **레코드 집합** 으로 **DataSource** Microsoft DataGrid 컨트롤 형식에 따라서에 대 한 데이터를 쉽게 표시할 수 있습니다를 **레코드 집합** 에 폼입니다.  
  
 두 번째 단추를 클릭 **검사 데이터**입니다. 이 실행 합니다 **ExamineData** 서브루틴입니다.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 다양 한 메서드 및 속성을 사용 하는 **레코드 집합** 데이터에 대 한 정보를 표시 하는 개체를 **레코드 집합**합니다. 사용 하 여 레코드의 수를 보고 하는 **RecordCount** 속성입니다. 반복 하 고는 **레코드 집합** 값을 인쇄 하 고는 **AbsolutePosition** 양식에 표시 텍스트 상자에는 속성입니다. 루프의 값에도 하는 동안를 **책갈피** 세 번째 레코드에 대 한 속성은 variant 변수인에 배치 됩니다 *vBookmark*, 나중에 사용할 수 있습니다.  
  
 루틴은 이전에 저장 하는 책갈피 변수를 사용 하 여 세 번째 레코드를 다시 직접 이동 합니다. 일상적인 호출을 **WalkFields** 서브루틴을 반복 하는 **필드** 의 컬렉션을 **레코드 집합** 각각에 대 한 세부 정보를 표시 하 고 **필드**  컬렉션에 있습니다.  
  
 마지막으로, **ExamineData** 사용 하 여는 **필터** 속성을 **레코드 집합** 레코드만 화면에는 **CategoryId** 같음 2입니다. 이 필터를 적용 한 결과 폼에 눈금 표시에에서 즉시 표시 됩니다.  
  
 에 표시 되는 기능에 대 한 자세한 합니다 **ExamineData** 서브루틴을 참조 하세요 [데이터 검사](../../../ado/guide/data/examining-data.md)합니다.  
  
 다음으로, 세 번째 단추를 클릭 **데이터 편집**합니다. 이렇게 하면 실행 합니다 **EditData** 서브루틴입니다.  
  
## <a name="editdata"></a>EditData  
 코드를 입력 하는 경우는 **EditData** 서브루틴을 합니다 **레코드 집합** 기준으로 계속 필터링 됩니다 **CategoryId** 필터 조건을 충족 하는 항목만 되도록 2, 같음 볼 수 있습니다. 먼저 반복 하 고는 **레코드 집합** 에 표시 되는 각 항목의 가격을 높이고 합니다 **레코드 집합** 10%입니다. 값을 **가격** 필드를 설정 하 여 변경 되는 **값** 새, 유효한 시간을 해당 필드에 대 한 속성.  
  
 유의 해야 합니다 **레코드 집합** 데이터 원본에서 연결이 끊어졌습니다. 수행한 변경 내용을 **EditData** 데이터의 로컬에 캐시 된 복사본에만 적용 됩니다. 자세한 내용은 [데이터 편집](../../../ado/guide/data/editing-data.md)합니다.  
  
 변경 내용을 걸 수 없습니다 데이터 원본에서 네 번째 단추를 클릭할 때까지 **업데이트 데이터**입니다. 이렇게 하면 실행 합니다 **UpdateData** 서브루틴입니다.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData에 적용 된 필터를 먼저 제거 합니다 **레코드 집합**합니다. 코드를 제거 하 고 다시 설정 `m_oRecordset1` 으로 **DataSource** 양식의 Microsoft 바인딩된 DataGrid에 대 한 있도록는 필터링 되지 않은 **레코드 집합** 표에 나타납니다.  
  
 코드를 확인 하는지 여부를 이동할 수 있습니다 뒤로 합니다 **레코드 집합** 를 사용 하 여는 **지원** 메서드를 **adMovePrevious** 인수입니다.  
  
 루틴을 사용 하 여 첫 번째 레코드를 이동 합니다 **MoveFirst** 메서드를 사용 하 여 필드의 원래 및 현재 값이 표시 됩니다는 **OriginalValue** 하 고 **값** 속성을 **필드** 개체입니다. 이러한 속성을 함께 합니다 **UnderlyingValue** (여기서 사용된 되지 않음)는 속성에 대해서는 설명 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.  
  
 다음으로 새 **연결** 개체가 생성 되 고 데이터 원본에 연결을 다시 설정 하는 데 사용 됩니다. 다시 연결 하면를 **레코드 집합** 새 설정 하 여 데이터 원본에 **연결** 으로 **ActiveConnection** 에 대 한 합니다 **레코드 집합**합니다. 코드를 호출 하 여 서버에 업데이트를 보낼 **UpdateBatch** 에 **레코드 집합**합니다.  
  
 일괄 업데이트에 성공 하면 모듈 수준 플래그 변수로 `m_flgPriceUpdated`를 True로 설정 됩니다. 이 데이터베이스에 대 한 모든 변경 내용을 정리 나중에 알립니다.  
  
 마지막으로 코드를 다시 이동의 첫 번째 레코드는 **레코드 집합** 원래 및 현재 값이 표시 됩니다. 값은 동일한를 호출한 후 **UpdateBatch**합니다.  
  
 데이터를 업데이트 하는 방법에 대 한 자세한 정보에 대 한 경우 수행할 작업을 포함 하는 동안 서버 변경 내용에 대 한 데이터에 **레코드 집합** 가 참조 연결이 끊긴 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.  
  
## <a name="formunload"></a>Form_Unload  
 합니다 **Form_Unload** 서브루틴은 여러 가지 이유로 중요 합니다. 첫째, 샘플 응용 프로그램 이므로 form_unload 응용 프로그램이 종료 되기 전에 데이터베이스에 대 한 변경 내용을 합니다. 둘째, 코드 명령을 개방적이 고에서 직접 실행 하는 방법을 보여줍니다 **연결** 사용 하 여 개체를 **Execute** 메서드. 마지막으로, 데이터 원본에 대 한 행 반환 하지 않는 쿼리 (업데이트 쿼리)를 실행 하는 예를 보여줍니다.
