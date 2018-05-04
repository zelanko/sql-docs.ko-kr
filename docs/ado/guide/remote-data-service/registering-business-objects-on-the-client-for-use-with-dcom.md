---
title: DCOM을 사용 하기 위해 클라이언트에서 비즈니스 개체에 등록 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 75a21910-607f-463a-ae18-a17130dafb7e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c92544630110443b3db9092738978a3608e57db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="registering-business-objects-on-the-client-for-use-with-dcom"></a>DCOM을 사용 하기 위해 클라이언트에서 비즈니스 개체에 등록
사용자 지정 비즈니스 개체는 클라이언트 쪽 DCOM을 통해 사용할 수 있는 식별자 (CLSID)를 해당 프로그램 이름 progid (프로그램)를 매핑할 수 있는지 확인 해야 합니다. 이러한 이유로 DCOM 개체의 ProgID 클라이언트 레지스트리에 여야 하며 서버 쪽 비즈니스 개체의 클래스 ID에 매핑됩니다. 다른 지원 되는 프로토콜 (HTTP, HTTPS 및 프로세스)이 필요는 없습니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 예를 들어 여는 특정 클래스 ID로, 예를 들어, "{00112233-4455-6677-8899-00aabbccddee}" 같은, MyBObj 라는 서버 쪽 비즈니스 개체를 노출 하는 경우 클라이언트 레지스트리에 다음 항목이 추가 되었는지 확인 합니다.  
  
```  
[HKEY_CLASSES_ROOT]  
\MyBObj\Clsid\(Default) "{00112233-4455-6677-8899-00AABBCCDDEE}"  
```


