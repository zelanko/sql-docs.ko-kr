---
title: onError 이벤트 (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onError event [ADO]
ms.assetid: b01cbc62-fbd7-4068-b16c-8b0f80a05887
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ccc57f9c034bfc0bd07d2e88394d09b7c766153a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47648061"
---
# <a name="onerror-event-rds"></a>onError 이벤트(RDS)
합니다 **onError** 이벤트 작업 중에 오류가 발생할 때마다 호출 됩니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
onError SCode, Description, Source, CancelDisplay  
```  
  
#### <a name="parameters"></a>매개 변수  
 *SCode*  
 오류의 상태 코드를 나타내는 정수입니다.  
  
 *Description*  
 A **문자열** 오류에 대 한 설명을 나타냅니다.  
  
 *원본*  
 A **문자열** 쿼리 또는 오류를 발생 시키는 명령을 나타내는입니다.  
  
 *CancelDisplay*  
 A **부울** 값에 설정 된 경우에는 **True**, 대화 상자에 표시 되지 않도록 오류를 방지 하는 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataControl 개체(RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>관련 항목  
 [ADO 이벤트 모델 예제 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 이벤트 처리기 요약](../../../ado/guide/data/ado-event-handler-summary.md)


