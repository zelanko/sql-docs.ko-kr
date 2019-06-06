---
title: CreateRecordset 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e0ac86f4ceac4c806bfa3f6df5cc9e2024b4d03d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712587"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 메서드(RDS)
빈 만듭니다 연결 끊김 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *개체*  
 나타내는 개체 변수를 [업데이트할](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 또는 [rds. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 *ColumnsInfos*  
 A **Variant** 의 각 열을 정의 하는 특성의 배열 합니다 **레코드 집합** 생성 합니다. 각 열 정의는 네 가지 필수 특성와 하나의 선택적 특성의 배열을 포함합니다.  
  
|attribute|설명|  
|---------------|-----------------|  
|이름|열 머리글의 이름입니다.|  
|형식|정수 데이터 형식입니다.|  
|크기|데이터 형식에 관계 없이 문자 너비의 정수입니다.|  
|Null 허용 여부|부울 값입니다.|  
|확장 (선택 사항)|이 선택적 특성 숫자 필드의 소수 자릿수를 정의합니다. 이 값을 지정 하지는 3 개의 확장에 숫자 값은 잘립니다. 전체 자릿수에 영향을 주지 않지만 소수점 이하의 자릿수를 3으로 잘립니다.|  
  
 열 배열 집합을 정의 하는 배열을로 그룹화 한 다음 합니다 **레코드 집합**합니다.  
  
## <a name="remarks"></a>Remarks  
 서버 쪽 비즈니스 개체에서 결과 채울 수 있습니다 **레코드 집합** 비-OLE DB 데이터 공급자에서 데이터와 같은 운영 체제 파일 주식 시세를 포함 합니다.  
  
 다음 표에서 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 에서 지원 되는 값을 **CreateRecordset** 메서드. 나열 된 번호 필드를 정의 하는 데 대 한 참조입니다.  
  
 각 데이터 형식에는 고정된 길이 또는 가변 길이입니다. 고정 길이 형식 크기가 미리 지정 된 크기 정의 여전히 필요 하기 때문에-1의 크기를 사용 하 여 정의 되어야 합니다. 가변 길이 데이터 형식에는 1에서 32767 사이의 크기를 허용합니다.  
  
 변수 데이터 형식 중 일부에 대 한 형식은 대체 열에 명시 된 형식으로 강제 변환할 수 있습니다. 표시 되지 것입니다 후 될 때까지 대체는 **레코드 집합** 만들어지고 채워집니다. 그런 다음 필요한 경우 실제 데이터 형식에 대해 확인할 수 있습니다.  
  
|길이|상수|Number|Substitution|  
|------------|--------------|------------|------------------|  
|고정|**adTinyInt**|16||  
|고정|**adSmallInt**|2||  
|고정|**adInteger**|3||  
|고정|**adBigInt**|20||  
|고정|**adUnsignedTinyInt**|17||  
|고정|**adUnsignedSmallInt**|18||  
|고정|**adUnsignedInt**|19||  
|고정|**adUnsignedBigInt**|21||  
|고정|**adSingle**|4||  
|고정|**adDouble**|5||  
|고정|**adCurrency**|6||  
|고정|**adDecimal**|14||  
|고정|**adNumeric**|131||  
|고정|**adBoolean**|11||  
|고정|**adError**|10||  
|고정|**adGuid**|72||  
|고정|**adDate**|7||  
|고정|**adDBDate**|133||  
|고정|**adDBTime**|134||  
|고정|**adDBTimestamp**|135|7|  
|변수|**adBSTR**|8|130|  
|변수|**adChar**|129|200|  
|변수|**adVarChar**|200||  
|변수|**adLongVarChar**|201|200|  
|변수|**adWChar**|130||  
|변수|**adVarWChar**|202|130|  
|변수|**adLongVarWChar**|203|130|  
|변수|**adBinary**|128||  
|변수|**adVarBinary**|204||  
|변수|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>관련 항목  
 [CreateRecordset 메서드 예제 (VB)](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [CreateRecordset 메서드 예제 (VBScript)](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [CreateObject 메서드(RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)



