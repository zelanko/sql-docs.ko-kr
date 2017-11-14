---
title: "HelloData에 대 한 설명 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b84d5aef9958c15682c6aeae2942487f30a6581
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="comments-on-hellodata"></a>HelloData에 대 한 설명
HelloData 응용 프로그램이 일반적인 ADO 응용 프로그램의 기본 작업을 단계별로: 가져오기, 검사, 편집 및 데이터를 업데이트 합니다. 응용 프로그램을 시작 하는 경우 첫 번째 단추를 클릭 **데이터 가져오기**합니다. 이렇게 하면 실행은 **GetData** 서브루틴 합니다.  
  
## <a name="getdata"></a>GetData  
 **GetData** 모듈 수준 변수만에 올바른 연결 문자열을 저장 하 고 *m_sConnStr*합니다. 연결 문자열에 대 한 자세한 내용은 참조 [연결 문자열 만들기](../../../ado/guide/data/creating-a-connection-string.md)합니다.  
  
 Visual Basic을 사용 하 여 오류 처리기를 할당 **OnError** 문. Ado에서 오류 처리에 대 한 자세한 내용은 참조 [의 오류 처리](../../../ado/guide/data/error-handling.md)합니다. 새 **연결** 개체가 만들어지면 및 **앞** 속성이 **adUseClient** HelloData 예제 만들기 때문에  *연결이 끊긴 레코드 집합*합니다. 즉, 데이터 원본에서 데이터를 가져온, 데이터 소스와 물리적 연결이 끊어진 하지만 로컬로 캐시 된 데이터가 계속 작업할 수는 즉시 사용자 **레코드 집합** 개체입니다.  
  
 연결이 열린 후 변수 (sSQL)에 SQL 문자열을 할당 합니다. 다음의 새 인스턴스를 만들고 **레코드 집합** 개체 `m_oRecordset1`합니다. 다음 코드 줄에서 엽니다는 **레코드 집합** 를 기존 **연결**전달, `sSQL` 의 소스로 **레코드 집합**합니다. ADO SQL 문자열을 결정을 내리는 데 도움이 되 조건이 충족에 대 한 소스로 **레코드 집합** 전달 하 여 명령의 텍스트 정의 **adCmdText** 는 마지막인수에**레코드 집합 열기** 메서드. 이 줄도 설정 하는 **LockType** 및 **모두** 연관는 **레코드 집합**합니다.  
  
 코드 집합의 다음 줄은 **마샬링** 속성이 **adMarshalModifiedOnly**합니다. **마샬링** 레코드 중간 계층 (또는 웹 서버)로 마샬링되어야 나타냅니다. 마샬링에 대 한 자세한 내용은 COM 설명서를 참조 합니다. 사용 하는 경우 **adMarshalModifiedOnly** 클라이언트 쪽 커서 ([앞](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)에 수정 된 레코드만 클라이언트는 중간 계층에 다시 기록 됩니다. 설정 **마샬링** 를 **adMarshalModifiedOnly** 마샬링 되므로 적은 수의 행 때문에 성능을 향상 시킬 수 있습니다.  
  
 다음으로 분리는 **레코드 집합** 설정 하 여 해당 **ActiveConnection** 속성에 **Nothing**합니다. 자세한 내용은 "연결을 해제 및 다시 연결 하는 레코드 집합" 섹션을 참조 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.  
  
 데이터 원본 연결을 닫고 소멸 시킵니다. 기존 **연결** 개체입니다. 이 사용 되는 리소스를 해제 합니다.  
  
 설정 하는 마지막 단계는 **레코드 집합** 로 **DataSource** Microsoft DataGrid 컨트롤 형식에 하므로 하는 데이터를 쉽게 표시할 수 있습니다는 **레코드 집합** 에 폼입니다.  
  
 두 번째 단추를 클릭 **데이터 검사**합니다. 이 실행 되는 **ExamineData** 서브루틴 합니다.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 다양 한 메서드와 속성을 사용 하는 **레코드 집합** 개체의 데이터에 대 한 정보를 표시 하는 **레코드 집합**합니다. 사용 하 여 레코드의 수를 보고는 **RecordCount** 속성입니다. 반복는 **레코드 집합** 의 값을 출력 하 고는 **AbsolutePosition** 속성 폼에 표시 텍스트 상자에 있습니다. 또한 while 루프의 값에는 **책갈피** 세 번째 레코드에 대 한 속성을 variant 변수에 배치 됩니다 *vBookmark*, 나중에 사용할 수 있습니다.  
  
 루틴은 이전에 저장 하는 책갈피 변수를 사용 하 여 세 번째 레코드에 다시 직접 이동 합니다. 일상적인 호출은 **WalkFields** 서브루틴을 반복 하는 **필드** 의 컬렉션은 **레코드 집합** 각각에 대 한 세부 정보를 표시 하 고 **필드**  컬렉션에 있습니다.  
  
 마지막으로, **ExamineData** 사용 하 여는 **필터** 의 속성에서 **레코드 집합** 레코드만 대 한 화면에는 **CategoryId** 같음 2입니다. 이 필터를 적용 한 결과 폼에 눈금 표시에에서 즉시 표시 됩니다.  
  
 에 표시 되는 기능에 대 한 자세한 내용은 **ExamineData** 서브루틴 참조 [데이터 검사](../../../ado/guide/data/examining-data.md)합니다.  
  
 다음 세 번째 단추 클릭 **데이터 편집**합니다. 이렇게 하면 실행은 **EditData** 서브루틴 합니다.  
  
## <a name="editdata"></a>EditData  
 코드 들어가면는 **EditData** 서브루틴은 **레코드 집합** 여전히에 필터링 되어 **CategoryId** 하는 필터 조건을 충족 하는 항목만 2, 같음 볼 수 있습니다. 먼저 반복의 **레코드 집합** 에 표시 되는 각 항목의 가격이 증가 하 고는 **레코드 집합** 10%입니다. 값은 **가격** 필드를 설정 하 여 변경에서 **값** 속성을 유효한 새 가격 같은 해당 필드에 대 한 합니다.  
  
 에 유의 해야는 **레코드 집합** 데이터 원본에서 연결이 끊어졌습니다. 변경한 내용을 **EditData** 데이터의 로컬에 캐시 된 복사본에만 적용 됩니다. 자세한 내용은 참조 [데이터 편집](../../../ado/guide/data/editing-data.md)합니다.  
  
 변경 내용을 걸 수 없습니다 데이터 원본에서 네 번째 단추를 클릭할 때까지 **데이터 업데이트**합니다. 이렇게 하면 실행은 **UpdateData** 서브루틴 합니다.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData에 적용 된 필터를 먼저 제거는 **레코드 집합**합니다. 제거 하 고 다시 설정 하는 코드 `m_oRecordset1` 으로 **DataSource** 폼에 바인딩된 datagrid Microsoft 있도록는 필터링 되지 않은 **레코드 집합** 눈금에 표시 합니다.  
  
 코드는 다음 확인 여부 있습니다 수 뒤로 이동 하는 **레코드 집합** 를 사용 하 여는 **지원** 메서드는 **adMovePrevious** 인수입니다.  
  
 루틴을 사용 하 여 첫 번째 레코드를 이동는 **MoveFirst** 메서드를 사용 하 여 필드의 원래 및 현재 값이 표시 됩니다는 **OriginalValue** 및 **값** 속성은 **필드** 개체입니다. 와 함께 이러한 속성은 **UnderlyingValue** (사용된 되지 않음 여기) 속성에 대해서는 설명 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.  
  
 다음, 새 **연결** 개체가 생성 되 고 데이터 원본에 연결을 다시 설정 하는 데 사용 합니다. 다시 연결 하면는 **레코드 집합** 새 설정 하 여 데이터 원본에 **연결** 로 **ActiveConnection** 에 대 한는 **레코드 집합**합니다. 코드를 호출 하 여 서버에는 업데이트를 보내는 **UpdateBatch** 에 **레코드 집합**합니다.  
  
 일괄 처리 업데이트에 성공 하면 모듈 수준 플래그가 변수 `m_flgPriceUpdated`, True로 설정 합니다. 알려이 나중에 데이터베이스에 대 한 모든 변경 내용을 정리 됩니다.  
  
 마지막으로, 코드로 다시 이동의 첫 번째 레코드는 **레코드 집합** 원래 및 현재 값이 표시 됩니다. 값이를 호출한 후 같은 **UpdateBatch**합니다.  
  
 데이터를 업데이트 하는 방법에 대 한 자세한 내용은 방법를 포함 하는 동안 서버 변경 내용에 대 한 데이터 프로그램 **레코드 집합** 은 참조 연결이 끊어질 [업데이트 및 데이터 유지](../../../ado/guide/data/updating-and-persisting-data.md)합니다.  
  
## <a name="formunload"></a>Form_Unload  
 **Form_Unload** 서브루틴은 여러 가지 이유로 중요 합니다. 첫째, 샘플 응용 프로그램 이므로 form_unload 응용 프로그램 종료 되기 전에 데이터베이스에 대 한 변경 내용이 있습니다. 둘째, 코드에 표시 된 명령을 열린에서 직접 실행 하는 방법을 **연결** 사용 하 여 개체는 **Execute** 메서드. 마지막으로 실행 데이터 원본에 대해 행을 반환 아닌 쿼리 (업데이트 쿼리) 예제를 보여 줍니다.

