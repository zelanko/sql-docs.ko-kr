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
manager: jroth
ms.openlocfilehash: 0f9efa743e6e5f9efe99e08001980ab87bf13247
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695228"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
ADO에서 런타임 오류 유형을 지정합니다.  
  
 오류 번호의 세 가지 양식은 나열 됩니다.  
  
-   양의 10 진수의 낮은 두 바이트 10 진수 형식의 전체 개수입니다. 이 번호는 기본 Visual Basic 오류 메시지 대화 상자에 표시 됩니다. 예를 들어, 런타임 오류가 발생 했습니다 '3707'.  
  
-   전체 오류 수의 10 진수의 10 진수 변환을 음수입니다.  
  
-   전체 오류 번호의 16 진수는 16 진수 표현입니다. Windows 기능 코드는 네 번째 숫자입니다. ADO 오류 번호에 대 한 기능 코드 *는*합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. 0x800***A***0E7B.  
  
> [!NOTE]
>  OLE DB 오류 ADO 응용 프로그램에 전달할 수 있습니다. 일반적으로 Windows 기능 코드의로 식별할 수 있습니다 *4*합니다. 예를 들어, 0x800***4***합니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707 -2146824581 0x800A0E7B|변경할 수 없습니다는 **ActiveConnection** 의 속성을 **레코드 집합** 있는 개체를 **명령** 원본으로 개체입니다.|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|서버 작업을 완료할 수 없습니다.|  
|**adErrCantChangeConnection**|3748 -2146824540 0x800A0EA4|연결이 거부 되었습니다. 새 연결 요청에 이미 사용 하는 것 보다 다양 한 특징이 있습니다.|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|제공 된 공급자는 이미 사용 하는 것에서 서로 다릅니다.|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|부호 불일치 또는 데이터 오버플로가 아닌 다른 이유로 데이터 값을 변환할 수 없습니다. 예를 들어, 변환 시 데이터가 잘렸습니다.|  
|**adErrCantCreate**|3725 -2146824563 0x800A0E8D|데이터 값을 설정 하거나 필드 데이터 형식을 알 되었거나 공급자가 작업을 수행 하려면 리소스 부족 하기 때문에 검색 될 수 없습니다.|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|작업을 수행 하려면 올바른 **ParentCatalog**합니다.|  
|**adErrColumnNotOnThisRow**|3726 -2146824562 0x800A0E8E|레코드에이 필드가 없습니다.|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|응용 프로그램이 현재 작업에 대 한 잘못 된 형식의 값을 사용합니다.|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|데이터 값 필드 데이터 형식으로 나타낼 수 너무 큽니다.|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|삭제할 개체의 URL은 현재 레코드의 범위를 벗어납니다.|  
|**adErrDenyNotSupported**|3750 -2146824538 0x800A0EA6|공급자는 공유 제한이 지원 하지 않습니다.|  
|**adErrDenyTypeNotSupported**|3751 -2146824537 0x800A0EA7|공급자는 요청 된 유형의 제한 공유를 지원 하지 않습니다.|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|개체 또는 공급자가 요청한 작업을 수행할 수 없습니다.|  
|**adErrFieldsUpdateFailed**|3749 -2146824539 0x800A0EA5|필드 업데이트 하지 못했습니다. 자세한 내용은 검토 합니다 **상태** 개별 필드 개체의 속성입니다.|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|이 컨텍스트에서 작업이 허용 되지 않습니다.|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|데이터 값 필드의 무결성 제약 조건과 충돌 합니다.|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**연결** 트랜잭션에서 하는 동안 개체를 명시적으로 닫을 수 없습니다.|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|인수는 잘못 된 형식의 적절 한 범위를 벗어난 또는 서로 충돌 합니다.|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|이 작업을 수행 하려면 연결을 사용할 수 없습니다. 연결이 닫혀 있거나 잘못 되었습니다.이 컨텍스트에서 것입니다.|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**매개 변수** 개체 잘못 정의 되었습니다. 불일치 하거나 불완전 한 정보를 제공 했습니다.|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|트랜잭션 조정 유효 하지 않거나 시작 되지 않았습니다.|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|URL에 잘못 된 문자가 있습니다. URL을 올바르게 입력 했는지 확인 합니다.|  
|**adErrItemNotFound**|3265 -2146825023 0x800A0CC1|요청된 된 이름 또는 서 수에 해당 하는 컬렉션의 항목을 찾을 수 없습니다.|  
|**adErrNoCurrentRecord**|3021 -2146825267 0x800A0BCD|어느 **BOF** 하거나 **EOF** True, 또는 현재 레코드를 삭제 합니다. 요청한 작업이 현재 레코드가 필요 합니다.|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|실행 하지 않는 동안 작업을 수행할 수 없습니다.|  
|**adErrNotReentrant**|3710 -2146824578 0x800A0E7E|이벤트를 처리 하는 동안 작업을 수행할 수 없습니다.|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|개체가 닫힐 때에 작업이 허용 되지 않습니다.|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|개체가는 컬렉션에 이미 있습니다. 추가할 수 없습니다.|  
|**adErrObjectNotSet**|3420 -2146824868 0x800A0D5C|개체가 유효 하지 않습니다.|  
|**adErrObjectOpen**|3705 -2146824583 0x800A0E79|개체가 열려 있을 때에 작업이 허용 되지 않습니다.|  
|**adErrOpeningFile**|3002 -2146825286 0x800A0BBA|파일을 열 수 없습니다.|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|사용자가 작업 취소 되었습니다.|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|작업을 수행할 수 없습니다. 공급자는 충분 한 저장소 공간을 가져올 수 없습니다.|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|권한 부족 필드에 쓸 수 없습니다.|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|공급자는 요청된 된 작업을 수행 하지 않았습니다.|  
|**adErrProviderNotFound**|3706 -2146824582 0x800A0E7A|공급자를 찾을 수 없습니다. 이 올바르게 설치 되지 합니다.|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|파일을 읽을 수 없습니다.|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|복사 작업을 수행할 수 없습니다. 개체가 명명 된 대상 URL에 이미 있습니다. 지정할 **adCopyOverwrite** 개체를 바꿀 수 있습니다.|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|지정된 된 URL을 나타내는 개체 하나 이상의 다른 프로세스에 의해 잠겨 있습니다. 프로세스가 완료 될 때까지 기다린 후 작업을 다시 시도 합니다.|  
|**adErrResourceOutOfScope**|3735 -2146824553 0x800A0E97|원본 또는 대상 URL 현재 레코드의 범위를 벗어납니다.|  
|**adErrSchemaViolation**|3722 -2146824566 0x800A0E8A|데이터 값의 데이터 형식 또는 필드의 제약 조건과 충돌 합니다.|  
|**adErrSignMismatch**|3723 -2146824565 0x800A0E8B|데이터 값은 부호가 있고 공급자가 사용한 필드 데이터 유형은 부호가 없기 때문에 변환에 실패 했습니다.|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|비동기적으로 연결 하는 동안 작업을 수행할 수 없습니다.|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|비동기적으로 실행 하는 동안 작업을 수행할 수 없습니다.|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|권한이 트리 또는 하위 트리를 액세스 하기에 충분 하지 않습니다.|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|작업이 완료 되지 않았습니다 하 고 상태를 사용할 수 없습니다. 필드를 사용할 수 없습니다 또는 작업을 시도 하지 않았습니다.|  
|**adErrUnsafeOperation**|3716 -2146824572 0x800A0E84|이 컴퓨터의 보안 설정이 다른 도메인의 데이터 원본 액세스를 방지 합니다.|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|원본 URL 또는 URL이 없는 대상의 부모입니다.|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|이 URL에 의해 명명 된 레코드가 없습니다.|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|공급자는 URL에서 표시 하는 저장 장치를 찾을 수 없습니다. URL을 올바르게 입력 했는지 확인 합니다.|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|파일에 쓰지 못했습니다.|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|내부 전용입니다. 사용하지 마십시오.|  
|**adWrnSecurityDialogHeader**|3718 -2146824570 0x800A0E86|내부 전용입니다. 사용하지 마십시오.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
 Wfc ADO의 다음 하위 집합만 정의 됩니다.  
  
|상수|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>적용 대상  
 [Number 속성(ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [ADO 오류 코드](../../../ado/guide/appendixes/ado-error-codes.md)
