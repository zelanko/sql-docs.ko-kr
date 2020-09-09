---
description: RemoveCertificate 메서드(ServerSettings 클래스)
title: RemoveCertificate 메서드 (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- RemoveCertificate Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 9ffdbc39-93f5-48fb-859a-86a3ad545827
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07ff32236bfb4b8eb26a7f0e9f8b891b77222ecb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544353"
---
# <a name="removecertificate-method-serversettings-class"></a>RemoveCertificate 메서드(ServerSettings 클래스)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  현재 보안 인증서를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.RemoveCertificate()  
```  
  
## <a name="parts"></a>부분  
 *object*  
 [인스턴스의 서버 설정을 나타내는](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) ServerSettings 클래스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]개체입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 U**int32** 값으로, 0은 서비스가 수정 되었음을 나타내고 1은 요청이 지원 되지 않음을 나타내며 다른 모든 숫자는 오류를 표시 합니다.  
  
## <a name="remarks"></a>설명  
  
## <a name="see-also"></a>참고 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
