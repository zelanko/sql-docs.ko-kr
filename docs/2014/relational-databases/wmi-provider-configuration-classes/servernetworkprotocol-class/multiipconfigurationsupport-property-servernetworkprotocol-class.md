---
title: MultiIpConfigurationSupport 속성 (ServerNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6f22b935a5c9ce0a78bb44d66d048889e8ac10dc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48166723"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 속성(ServerNetworkProtocol 클래스)
  서버 네트워크 프로토콜에서 여러 개의 IP 주소를 지원하는지 여부를 지정하는 부울 속성을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ProtocolName 속성 (ServerNetworkProtocol 클래스)](servernetworkprotocol-class.md) 의 인스턴스에 사용 되는 네트워크 프로토콜을 나타내는 개체 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 서버 네트워크 프로토콜에서 여러 개의 IP 주소를 지원하는지 여부를 지정하는 부울 값입니다. `true`는 서버 네트워크 프로토콜에서 여러 개의 IP 주소를 지원함을 나타내고 `false`는 서버 네트워크 프로토콜에서 여러 개의 IP 주소를 지원하지 않음을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [서버 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
