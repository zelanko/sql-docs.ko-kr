---
title: 별칭 속성(별칭 탭)
description: SQL Server 인스턴스에 연결할 때 대체 이름을 사용할 수 있도록 속성 대화 상자의 별칭 탭을 사용하여 별칭을 구성합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 2d1498e2-129c-4ce7-88e5-408e4037243c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 098da595a57c82e4d0ff68713880f38fe6acb6d2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902188"
---
# <a name="ltaliasgt-properties-alias-tab"></a>&lt;별칭&gt; 속성(별칭 탭)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

별칭은 연결 설정에 사용할 수 있는 대체 이름입니다. 별칭은 연결 문자열의 필수 요소를 캡슐화하고 사용자가 선택한 이름으로 나타납니다. **\<**Alias name**> 속성** 대화 상자의 **별칭** 페이지를 사용하여 별칭에 대한 연결 문자열의 요소를 확인하거나 지정할 수 있습니다.

## <a name="options"></a>옵션

**별칭**

이 연결을 나타내는 데 사용할 이름(별칭)입니다.  

**파이프 이름** / **포트 번호**  

연결 문자열의 추가 요소입니다. 이 상자의 이름은 선택한 프로토콜에 따라 달라집니다. 예는 아래 항목을 참조하십시오.  

**프로토콜**

연결에 사용된 프로토콜입니다.

**Server**

연결 중인 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.  

## <a name="see-also"></a>참고 항목

- [공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
- [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
- [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)