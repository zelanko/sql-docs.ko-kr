---
description: ADO 메서드
title: ADO 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: rothja
ms.author: jroth
ms.openlocfilehash: 10f9aaf7aefa87586df77dd0da5ac1be336d4f53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451385"
---
# <a name="ado-methods"></a>ADO 메서드

|메서드|설명|  
|-|-|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|업데이트할 수 있는 **레코드 집합** 개체에 대 한 새 레코드를 만듭니다.|  
|[Append](../../../ado/reference/ado-api/append-method-ado.md)|컬렉션에 개체를 추가 합니다. 컬렉션이 **필드인**경우 컬렉션에 추가 되기 전에 새 **필드** 개체를 만들 수 있습니다.|  
|[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)|대량 텍스트 또는 이진 데이터 **필드**또는 **매개 변수** 개체에 데이터를 추가 합니다.|  
|[BeginTrans, CommitTrans 및 RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)|는 다음과 같이 **Connection** 개체 내에서 트랜잭션 처리를 관리 합니다.<br /><br /> **BeginTrans** -새 트랜잭션을 시작 합니다.<br /><br /> **CommitTrans** -모든 변경 내용을 저장 하 고 현재 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.<br /><br /> **RollbackTrans** -모든 변경 내용을 취소 하 고 현재 트랜잭션을 종료 합니다. 새 트랜잭션을 시작할 수도 있습니다.|  
|[취소](../../../ado/reference/ado-api/cancel-method-ado.md)|보류 중인 비동기 메서드 호출의 실행을 취소 합니다.|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|보류 중인 일괄 처리 업데이트를 취소 합니다.|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|**Update** 메서드를 호출 하기 전에 레코드 **집합** 개체의 현재 행 또는 새 행 또는 **Record** 개체의 **Fields** 컬렉션에 적용 된 모든 변경 내용을 취소 합니다.|  
|[지우기](../../../ado/reference/ado-api/clear-method-ado.md)|**Errors** 컬렉션에서 **오류** 개체를 모두 제거 합니다.|  
|[복제](../../../ado/reference/ado-api/clone-method-ado.md)|기존 **recordset** 개체에서 중복 **레코드 집합** 개체를 만듭니다. 필요에 따라 복제본을 읽기 전용으로 지정 합니다.|  
|[닫기](../../../ado/reference/ado-api/close-method-ado.md)|열린 개체와 모든 종속 개체를 닫습니다.|  
|[CompareBookmarks](../../../ado/reference/ado-api/comparebookmarks-method-ado.md)|두 책갈피를 비교 하 여 상대 값의 표시를 반환 합니다.|  
|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md)|파일이 나 디렉터리와 해당 내용을 다른 위치로 복사 합니다.|  
|[CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md)|**스트림에** 따라 지정 된 문자 또는 바이트 수를 다른 **스트림** 개체에 복사 합니다. **Type**|  
|[CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md)|지정 된 속성을 가진 새 **매개 변수** 개체를 만듭니다.|  
|[Delete (ADO 매개 변수 컬렉션)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)|**Parameters** 컬렉션에서 개체를 삭제 합니다.|  
|[Delete (ADO Fields Collection)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)|**Fields** 컬렉션에서 개체를 삭제 합니다.|  
|[Delete (ADO 레코드 집합)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|현재 레코드 또는 레코드 그룹을 삭제 합니다.|  
|[DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md)|파일이 나 디렉터리와 모든 하위 디렉터리를 삭제 합니다.|  
|[Execute (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)|**CommandText** 속성에 지정 된 쿼리, SQL 문 또는 저장 프로시저를 실행 합니다.|  
|[Execute (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|지정 된 쿼리, SQL 문, 저장 프로시저 또는 공급자별 텍스트를 실행 합니다.|  
|[찾아낼](../../../ado/reference/ado-api/find-method-ado.md)|**레코드 집합** 에서 지정 된 조건을 만족 하는 행을 검색 합니다.|  
|[플러시](../../../ado/reference/ado-api/flush-method-ado.md)|ADO 버퍼에 남아 있는 **스트림의** 내용을 **스트림이** 연결 된 기본 개체에 강제로 적용 합니다.|  
|[get_OLEDBCommand 메서드](../../../ado/reference/ado-api/get-oledbcommand-method.md)|먼저 ADO 명령에 설정 된 모든 매개 변수 정보를 OLEDB 명령에 전파 하는 기본 OLEDB 명령을 반환 합니다.|  
|[GetChildren](../../../ado/reference/ado-api/getchildren-method-ado.md)|이 **레코드가**나타내는 디렉터리의 파일 및 하위 디렉터리를 나타내는 행을 포함 하는 **레코드 집합** 을 반환 합니다.|  
|[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)|크게 텍스트 또는 이진 데이터 **필드** 개체의 내용을 모두 또는 일부 반환 합니다.|  
|[GetDataProviderDSO 메서드](../../../ado/reference/ado-api/getdataproviderdso-method.md)|셰이프 공급자에서 내부 OLEDB 데이터 원본 개체를 검색 합니다.|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|**레코드 집합** 개체의 여러 레코드를 배열로 검색 합니다.|  
|[GetString](../../../ado/reference/ado-api/getstring-method-ado.md)|**레코드 집합** 을 문자열로 반환 합니다.|  
|[LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)|기존 파일의 내용을 **스트림으로**로드 합니다.|  
|[이동](../../../ado/reference/ado-api/move-method-ado.md)|**레코드 집합** 개체에서 현재 레코드의 위치를 이동 합니다.|  
|[MoveFirst, MoveLast, MoveNext 및 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|지정 된 **레코드 집합** 개체에서 첫 번째, 마지막, 다음 또는 이전 레코드로 이동 하 고이 레코드를 현재 레코드로 설정 합니다.|  
|[MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)|파일이 나 디렉터리와 해당 내용을 다른 위치로 이동 합니다.|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|현재 **레코드 집합** 개체를 지우고 일련의 명령으로 이동 하 여 다음 **레코드 집합** 을 반환 합니다.|  
|[Open (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)|데이터 원본에 대 한 연결을 엽니다.|  
|[Open (ADO 레코드)](../../../ado/reference/ado-api/open-method-ado-record.md)|기존 **Record** 개체를 열거나 새 파일이 나 디렉터리를 만듭니다.|  
|[열기 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|커서를 엽니다.|  
|[Open (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)|이진 또는 텍스트 데이터 스트림을 조작 하는 **Stream** 개체를 엽니다.|  
|[OpenSchema](../../../ado/reference/ado-api/openschema-method.md)|공급자에서 데이터베이스 스키마 정보를 가져옵니다.|  
|[put_OLEDBCommand 메서드](../../../ado/reference/ado-api/put-oledbcommand-method.md)|이 메서드는 작업을 수행 하지 않으며 항상 S_OK 반환 합니다.|  
|[읽기](../../../ado/reference/ado-api/read-method.md)|**스트림** 개체에서 지정 된 바이트 수를 읽습니다.|  
|[ReadText](../../../ado/reference/ado-api/readtext-method.md)|텍스트 **스트림** 개체에서 지정 된 수의 문자를 읽습니다.|  
|[새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md)|공급자와 관련 하 여 사용 가능한 개체를 반영 하도록 컬렉션의 개체를 업데이트 합니다.|  
|[매크로](../../../ado/reference/ado-api/requery-method.md)|개체의 기반이 되는 쿼리를 다시 실행 하 여 **레코드 집합** 개체의 데이터를 업데이트 합니다.|  
|[다시 동기화](../../../ado/reference/ado-api/resync-method.md)|현재 레코드 **집합** 개체 또는 **Record** 개체의 **Fields** 컬렉션에 있는 데이터를 기본 데이터베이스에서 새로 고칩니다.|  
|[저장](../../../ado/reference/ado-api/save-method.md)|파일 또는 **스트림** 개체에 **레코드 집합** 을 저장 합니다.|  
|[SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)|**스트림의** 이진 콘텐츠를 파일에 저장 합니다.|  
|[Seek](../../../ado/reference/ado-api/seek-method.md)|**레코드 집합** 의 인덱스를 검색 하 여 지정 된 값과 일치 하는 행을 빠르게 찾고 현재 행 위치를 해당 행으로 변경 합니다.|  
|[SetEOS](../../../ado/reference/ado-api/seteos-method.md)|스트림의 끝 위치를 설정 합니다.|  
|[SkipLine](../../../ado/reference/ado-api/skipline-method.md)|텍스트 스트림을 읽을 때 한 줄 전체를 건너뜁니다.|  
|[우편함](../../../ado/reference/ado-api/stat-method.md)|열려 있는 스트림에 대 한 통계 정보를 가져옵니다.|  
|[지원](../../../ado/reference/ado-api/supports-method.md)|지정 된 **레코드 집합** 개체가 특정 유형의 기능을 지원 하는지 여부를 확인 합니다.|  
|[Update](../../../ado/reference/ado-api/update-method.md)|레코드 **집합** 개체의 현재 행 또는 **Record** 개체의 **Fields** 컬렉션에 대 한 변경 내용을 저장 합니다.|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|모든 보류 중인 일괄 처리 업데이트를 디스크에 기록 합니다.|  
|[쓰기](../../../ado/reference/ado-api/write-method.md)|**스트림** 개체에 이진 데이터를 씁니다.|  
|[WriteText](../../../ado/reference/ado-api/writetext-method.md)|지정 된 텍스트 문자열을 **스트림** 개체에 씁니다.|  
  
## <a name="see-also"></a>관련 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)   
 [ADO 컬렉션](../../../ado/reference/ado-api/ado-collections.md)   
 [ADO 동적 속성](../../../ado/reference/ado-api/ado-dynamic-properties.md)   
 [ADO 열거 상수](../../../ado/reference/ado-api/ado-enumerated-constants.md)   
 [부록 B: ADO 오류](../../../ado/guide/appendixes/appendix-b-ado-errors.md)   
 [ADO 이벤트](../../../ado/reference/ado-api/ado-events.md)   
 [ADO 개체 모델](../../../ado/reference/ado-api/ado-object-model.md)   
 [ADO 개체 및 인터페이스](../../../ado/reference/ado-api/ado-objects-and-interfaces.md)   
 [ADO 속성](../../../ado/reference/ado-api/ado-properties.md)
