---
title: ErrorValueEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18117be8dccc64f7ed2583170cf062145836f337
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932870"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
ADO 런타임 오류의 유형을 지정 합니다.  
  
 다음 세 가지 형식의 오류 번호가 나열 됩니다.  
  
-   양의 10 진수-10 진수 형식의 전체 숫자의 하위 2 바이트입니다. 이 번호는 기본 Visual Basic 오류 메시지 대화 상자에 표시 됩니다. 예를 들어 런타임 오류 ' 3707 '입니다.  
  
-   음수 10 진수-전체 오류 번호의 10 진수 변환입니다.  
  
-   16 진수-전체 오류 번호의 16 진수 표현입니다. Windows 기능 코드는 네 번째 숫자입니다. ADO 오류 번호에 대 한 기능 코드 *는입니다.* 예: 0x800***A***0e7b  
  
> [!NOTE]
>  OLE DB 오류가 ADO 응용 프로그램으로 전달 될 수 있습니다. 일반적으로 Windows 기능 코드 *4*로 식별할 수 있습니다. 예를 들면 0x800***4***입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707-2146824581 0x800A0E7B|**Command** 개체를 원본으로 포함 하는 **레코드 집합** 개체의 **ActiveConnection** 속성을 변경할 수 없습니다.|  
|**adErrCannotComplete**|3732-2146824556 0x800A0E94|서버에서 작업을 완료할 수 없습니다.|  
|**adErrCantChangeConnection**|3748-2146824540 0x800A0EA4|연결이 거부 되었습니다. 요청 된 새 연결에 이미 사용 중인 것과 다른 특징이 있습니다.|  
|**adErrCantChangeProvider**|3220-2146825068 0X800A0C94|제공 된 공급자가 이미 사용 중인 공급자와 다릅니다.|  
|**adErrCantConvertvalue**|3724-2146824564 0x800A0E8C|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 인해 데이터 값을 변환할 수 없습니다. 예를 들어 변환은 데이터를 잘랐습니다.|  
|**adErrCantCreate**|3725-2146824563 0x800A0E8D|필드 데이터 형식을 알 수 없거나 공급자가 작업을 수행할 수 있는 리소스가 부족 하 여 데이터 값을 설정 하거나 검색할 수 없습니다.|  
|**adErrCatalogNotSet**|3747-2146824541 0x800A0EA3|작업에 올바른 **ParentCatalog**가 필요 합니다.|  
|**adErrColumnNotOnThisRow**|3726-2146824562 0x800A0E8E|레코드에이 필드가 없습니다.|  
|**adErrDataConversion**|3421-2146824867 0x800A0D5D|응용 프로그램에서 현재 작업에 잘못 된 형식의 값을 사용 합니다.|  
|**adErrDataOverflow**|3721-2146824567 0x800A0E89|데이터 값이 너무 커서 필드 데이터 형식으로 나타낼 수 없습니다.|  
|**adErrDelResOutOfScope**|3738-2146824550 0x800A0E9A|삭제할 개체의 URL이 현재 레코드의 범위를 벗어났습니다.|  
|**adErrDenyNotSupported**|3750-2146824538 0x800A0EA6|공급자는 공유 제한을 지원 하지 않습니다.|  
|**adErrDenyTypeNotSupported**|3751-2146824537 0x800A0EA7|공급자가 요청 된 공유 제한 종류를 지원 하지 않습니다.|  
|**adErrFeatureNotAvailable**|3251-2146825037 0x800A0CB3|개체 또는 공급자가 요청한 작업을 수행할 수 없습니다.|  
|**adErrFieldsUpdateFailed**|3749-2146824539 0x800A0EA5|필드를 업데이트 하지 못했습니다. 자세한 내용은 개별 field 개체의 **Status** 속성을 확인 하세요.|  
|**adErrIllegalOperation**|3219-2146825069 0x800A0C93|이 컨텍스트에서는 작업을 수행할 수 없습니다.|  
|**Aderrsilent Ity위반**|3719-2146824569 0x800A0E87|데이터 값이 필드의 무결성 제약 조건과 충돌 합니다.|  
|**adErrInTransaction**|3246-2146825042 0x800A0CAE|트랜잭션에서 **연결** 개체를 명시적으로 닫을 수 없습니다.|  
|**adErrInvalidArgument**|3001-2146825287 0x800A0BB9|인수가 잘못 된 형식 이거나, 허용 범위를 벗어났습니다. 또는 서로 충돌 합니다.|  
|**adErrInvalidConnection**|3709-2146824579 0x800A0E7D|이 작업을 수행 하는 데 연결을 사용할 수 없습니다. 이 컨텍스트에서 닫히거나 잘못 되었습니다.|  
|**adErrInvalidParamInfo**|3708-2146824580 0x800A0E7C|**매개 변수** 개체가 잘못 정의 되었습니다. 일관 되지 않거나 완전 하지 않은 정보가 제공 되었습니다.|  
|**adErrInvalidTransaction**|3714-2146824574 0x800A0E82|조정 트랜잭션이 잘못 되었거나 시작 되지 않았습니다.|  
|**adErrInvalidURL**|3729-2146824559 0x800A0E91|URL에 잘못 된 문자가 포함 되어 있습니다. URL을 올바르게 입력 했는지 확인 합니다.|  
|**adErrItemNotFound**|3265-2146825023 0x800A0CC1|컬렉션에서 요청 된 이름 또는 서 수에 해당 하는 항목을 찾을 수 없습니다.|  
|**adErrNoCurrentRecord**|3021-2146825267 0x800A0BCD|**BOF** 또는 **EOF** 가 True 이거나 현재 레코드가 삭제 되었습니다. 요청한 작업에는 현재 레코드가 필요 합니다.|  
|**adErrNotExecuting**|3715-2146824573 0x800A0E83|실행 하지 않는 동안에는 작업을 수행할 수 없습니다.|  
|**adErrNotReentrant**|3710-2146824578 0x800A0E7E|이벤트를 처리 하는 동안에는 작업을 수행할 수 없습니다.|  
|**adErrObjectClosed**|3704-2146824584 0x800A0E78|개체가 닫혀 있으면 작업을 수행할 수 없습니다.|  
|**adErrObjectInCollection**|3367-2146824921 0x800A0D27|개체가 이미 컬렉션에 있습니다. 을 추가할 수 없습니다.|  
|**adErrObjectNotSet**|3420-2146824868 0x800A0D5C|개체가 더 이상 유효 하지 않습니다.|  
|**adErrObjectOpen**|3705-2146824583 0x800A0E79|개체가 열려 있으면 작업을 수행할 수 없습니다.|  
|**adErrOpeningFile**|3002-2146825286 0x800A0BBA|파일을 열 수 없습니다.|  
|**adErrOperationCancelled**|3712-2146824576 0x800A0E80|사용자가 작업을 취소 했습니다.|  
|**adErrOutOfSpace**|3734-2146824554 0x800A0E96|작업을 수행할 수 없습니다. 공급자가 충분 한 저장소 공간을 얻을 수 없습니다.|  
|**Aderr이상 거부 됨**|3720-2146824568 0x800A0E88|권한이 부족 하 여 필드에 쓸 수 없습니다.|  
|**adErrProviderFailed**|3000-2146825288 0x800A0BB8|공급자가 요청한 작업을 수행 하지 않았습니다.|  
|**adErrProviderNotFound**|3706-2146824582 0x800A0E7A|공급자를 찾을 수 없습니다. 올바르게 설치 되지 않았을 수 있습니다.|  
|**adErrReadFile**|3003-2146825285 0x800A0BBB|파일을 읽을 수 없습니다.|  
|**adErrResourceExists**|3731-2146824557 0x800A0E93|복사 작업을 수행할 수 없습니다. 대상 URL에 의해 이름이 지정 된 개체가 이미 있습니다. **AdCopyOverwrite** 를 지정 하 여 개체를 바꿉니다.|  
|**adErrResourceLocked**|3730-2146824558 0x800A0E92|지정 된 URL이 나타내는 개체가 하나 이상의 다른 프로세스에 의해 잠겨 있습니다. 프로세스가 완료 될 때까지 기다렸다가 작업을 다시 시도 하십시오.|  
|**adErrResourceOutOfScope**|3735-2146824553 0x800A0E97|원본 또는 대상 URL이 현재 레코드 범위를 벗어났습니다.|  
|**adErrSchemaViolation**|3722-2146824566 0x800A0E8A|데이터 값이 필드의 데이터 형식 또는 제약 조건과 충돌 합니다.|  
|**adErrSignMismatch**|3723-2146824565 0x800A0E8B|데이터 값은 부호가 있고 공급자가 사용한 필드 데이터 형식은 부호가 없기 때문에 변환에 실패 했습니다.|  
|**adErrStillConnecting**|3713-2146824575 0x800A0E81|비동기 방식으로 연결 하는 동안에는 작업을 수행할 수 없습니다.|  
|**adErrStillExecuting**|3711-2146824577 0x800A0E7F|비동기적으로 실행 하는 동안에는 작업을 수행할 수 없습니다.|  
|**adErrTreePermissionDenied**|3728-2146824560 0x800A0E90|트리 또는 하위 트리에 액세스할 수 있는 권한이 부족 합니다.|  
|**adErrUnavailable 수 없음**|3736-2146824552 0x800A0E98|작업이 완료 되지 않았고 상태를 사용할 수 없습니다. 필드를 사용할 수 없거나 작업을 시도 하지 않았을 수 있습니다.|  
|**adErrUnsafeOperation**|3716-2146824572 0x800A0E84|이 컴퓨터의 안전 설정으로는 다른 도메인의 데이터 원본에 액세스할 수 없습니다.|  
|**adErrURLDoesNotExist**|3727-2146824561 0x800A0E8F|원본 URL 또는 대상 URL의 부모가 없습니다.|  
|**adErrURLNamedRowDoesNotExist**|3737-2146824551 0x800A0E99|이 URL로 이름이 지정 된 레코드가 없습니다.|  
|**adErrVolumeNotFound**|3733-2146824555 0x800A0E95|공급자가 URL로 지정 된 저장 장치를 찾을 수 없습니다. URL을 올바르게 입력 했는지 확인 합니다.|  
|**adErrWriteFile**|3004-2146825284 0x800A0BBC|파일에 쓰지 못했습니다.|  
|**adWrnSecurityDialog**|3717-2146824571 0x800A0E85|내부 전용입니다. 사용하지 마십시오.|  
|**adWrnSecurityDialogHeader**|3718-2146824570 0x800A0E86|내부 전용입니다. 사용하지 마십시오.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
 이에 해당 하는 ADO/WFC 하위 집합만 정의 됩니다.  
  
|상수|  
|--------------|  
|AdoEnums. ErrorValue. BOUNDTOCOMMAND|  
|AdoEnums. ErrorValue. DATACONVERSION|  
|AdoEnums. ErrorValue. FEATURENOTAVAILABLE|  
|AdoEnums. ErrorValue. ILLEGALOPERATION|  
|AdoEnums. ErrorValue. INTRANSACTION|  
|AdoEnums. ErrorValue. INVALIDARGUMENT|  
|AdoEnums 연결|  
|AdoEnums 값. INVALIDPARAMINFO|  
|AdoEnums 값. ITEMNOTFOUND|  
|AdoEnums. ErrorValue. NOCURRENTRECORD|  
|AdoEnums 값. NOTEXECUTING|  
|AdoEnums 값. NOTREENTRANT|  
|AdoEnums 값. OBJECTCLOSED|  
|AdoEnums 값. OBJECTINCOLLECTION|  
|AdoEnums. ErrorValue. OBJECTNOTSET|  
|AdoEnums 값. OBJECTOPEN|  
|AdoEnums 값이 취소 되었습니다.|  
|AdoEnums 값. PROVIDERNOTFOUND|  
|AdoEnums. ErrorValue. STILLCONNECTING|  
|AdoEnums. ErrorValue. STILLEXECUTING|  
|AdoEnums 값.|  
  
## <a name="applies-to"></a>적용 대상  
 [Number 속성(ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [ADO 오류 코드](../../../ado/guide/appendixes/ado-error-codes.md)
