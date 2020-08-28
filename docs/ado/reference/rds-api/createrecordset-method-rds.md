---
description: CreateRecordset 메서드(RDS)
title: CreateRecordset 메서드 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a459ddea3716bb918ed18a49d632e20a9e4557fd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982524"
---
# <a name="createrecordset-method-rds"></a>CreateRecordset 메서드(RDS)
연결 되지 않은 빈 [레코드 집합](../ado-api/recordset-object-ado.md)을 만듭니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Object*  
 DataFactory 또는 RDS를 나타내는 개체 변수 [RDSServer](./datafactory-object-rdsserver.md) . [ DataControl](./datacontrol-object-rds.md) 개체입니다.  
  
 *ColumnsInfos*  
 만든 **레코드 집합** 의 각 열을 정의 하는 특성의 **변형** 배열입니다. 각 열 정의에는 네 개의 필수 특성과 하나의 선택적 특성 배열을 포함 합니다.  
  
|attribute|설명|  
|---------------|-----------------|  
|Name|열 머리글의 이름입니다.|  
|Type|데이터 형식의 정수입니다.|  
|크기|데이터 형식과 관계 없이 문자 너비의 정수입니다.|  
|Null 허용 여부|부울 값을 지정합니다.|  
|크기 조정 (선택 사항)|이 선택적 특성은 숫자 필드에 대 한 소수 자릿수를 정의 합니다. 이 값을 지정 하지 않으면 숫자 값이 3 눈금으로 잘립니다. 전체 자릿수는 영향을 받지 않지만 소수점 뒤의 자릿수는 3으로 잘립니다.|  
  
 그런 다음 열 배열 집합을 **레코드 집합**을 정의 하는 배열로 그룹화 합니다.  
  
## <a name="remarks"></a>설명  
 서버 쪽 비즈니스 개체는 결과 **레코드 집합** 을 OLE DB 아닌 데이터 공급자 (예: 주식 시세를 포함 하는 운영 체제 파일)의 데이터로 채울 수 있습니다.  
  
 다음 표에서는 **CreateRecordset** 메서드에서 지 원하는 [DataTypeEnum](../ado-api/datatypeenum.md) 값을 보여 줍니다. 나열 된 숫자는 필드를 정의 하는 데 사용 되는 참조 번호입니다.  
  
 각 데이터 형식은 고정 길이 또는 가변 길이입니다. 고정 길이 형식은 크기를 미리 결정 하 고 크기 정의가 여전히 필요 하므로 크기가-1로 정의 되어야 합니다. 가변 길이 데이터 형식에는 1에서 32767 사이의 크기를 사용할 수 있습니다.  
  
 일부 변수 데이터 형식의 경우이 형식은 대체 열에 기록 된 형식으로 강제 변환할 수 있습니다. **레코드 집합** 을 만들고 채울 때까지 대체가 표시 되지 않습니다. 그런 다음 필요한 경우 실제 데이터 형식을 확인할 수 있습니다.  
  
|길이|상수|Number|대체|  
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

:::row:::
    :::column:::
        [DataControl 개체(RDS)](./datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataFactory 개체(RDSServer)](./datafactory-object-rdsserver.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [CreateRecordset 메서드 예제 (VB)](../ado-api/createrecordset-method-example-vb.md)   
 [CreateRecordset 메서드 예제 (VBScript)](./createrecordset-method-example-vbscript.md)   
 [CreateObject 메서드(RDS)](./createobject-method-rds.md)