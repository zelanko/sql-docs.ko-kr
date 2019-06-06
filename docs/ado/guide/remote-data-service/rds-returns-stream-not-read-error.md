---
title: RDS 반환 &quot;읽지 않았습니다 Stream&quot; 오류 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 598326335c32f18b5d7f5a764d387e5b5ea536f6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699431"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS 반환 &quot;읽지 않았습니다 Stream&quot; 오류
"Stream 개체 읽을 수 없습니다, 비어 있거나 현재 위치는 Stream의 끝 때문에 있습니다. 비어 있지 않은 스트림용 Position 속성을 사용 하 여 현재 위치를 설정 합니다. Stream 비어 있는지를 확인 하려면 크기 속성을 확인 합니다. "  
  
 이 오류 메시지를 표시 하는 경우 http를 통해 매개 변수화 된 계층적 쿼리를 사용 하려고 했습니다 수 있습니다. RDS는 원격 매개 변수가 있는 계층을 사용 하는 것을 허용 하지 않습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소는 더 이상 포함 된 Windows 운영 체제에서 (Windows 8을 참조 하 고 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/download/details.aspx?id=27416) 자세한). RDS 클라이언트 구성 요소는 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 [WCF 데이터 서비스](https://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [RDS 기본 사항](../../../ado/guide/remote-data-service/rds-fundamentals.md)


