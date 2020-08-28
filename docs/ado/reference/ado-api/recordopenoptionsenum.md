---
description: RecordOpenOptionsEnum
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: rothja
ms.author: jroth
ms.openlocfilehash: 352622f55e82b1941439a242249e067aae090e51
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989784"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
[레코드](./record-object-ado.md)를 열기 위한 옵션을 지정 합니다. 이러한 값은 또는을 사용 하 여 결합할 수 있습니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|공급자에 게 **레코드** 와 연결 된 필드를 처음에 검색 하지 않아도 되 고 처음에 필드에 액세스 하려고 할 때이를 검색할 수 있음을 나타냅니다. 이 플래그가 없음을 나타내는 기본 동작은 모든 **레코드** 개체 필드를 검색 하는 것입니다.|  
|**adDelayFetchStream**|0x4000|**레코드** 와 연결 된 기본 스트림을 처음에 검색할 필요가 없음을 공급자에 게 나타냅니다. 이 플래그가 없음을 나타내는 기본 동작은 **Record** 개체와 연결 된 기본 스트림을 검색 하는 것입니다.|  
|**adOpenAsync**|0x1000|**Record** 개체가 비동기 모드로 열려 있음을 나타냅니다.|  
|**adOpenExecuteCommand**|0x10000|소스 문자열에 실행 해야 하는 명령 텍스트가 포함 되어 있음을 나타냅니다. 이 값은 레코드 집합의 **Adcmdtext** 옵션과 동일 합니다 **. Open**.|  
|**adOpenRecordUnspecified 되지 않음**|-1|기본값 옵션이 지정 되지 않았음을 나타냅니다.|  
|**adOpenOutput**|0x800000|소스가 실행 가능한 스크립트를 포함 하는 노드 (예:)를 가리키는지 여부를 나타냅니다. ASP 페이지)를 선택한 후에는 실행 된 스크립트의 결과를 포함 하는 **레코드가** 열립니다. 이 값은 컬렉션이 아닌 레코드에만 사용할 수 있습니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 이러한 상수에는 ADO/WFC 해당 항목이 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [Open 메서드(ADO 레코드)](./open-method-ado-record.md)