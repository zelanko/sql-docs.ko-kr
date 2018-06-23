---
title: SetEnable 메서드 (ClientNetworkProtocol 클래스) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- SetEnable Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c158c2340731253e6e8595e6e83e4dbcc1c85c41
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180794"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>SetEnable 메서드(ClientNetworkProtocol 클래스)
  지정한 클라이언트 네트워크 프로토콜 설정의 [클라이언트 프로토콜 구성](http://technet.microsoft.com/library/ms181035.aspx)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object  
.SetEnableMethod()  
  
```  
  
## <a name="parts"></a>부분  
 *object*  
 A [ClientNetworkProtocol 클래스](clientnetworkprotocol-class.md) 에서 사용 하는 네트워크 프로토콜을 나타내는 개체는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 클라이언트입니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 `uint32` 값으로, 0은 서비스가 수정되었음을 나타내고 1은 요청이 지원되지 않음을 나타내며 다른 모든 숫자는 오류를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>관련 항목  
 [클라이언트 네트워크 프로토콜 및 네트워크 라이브러리 구성](http://technet.microsoft.com/library/ms181035.aspx)  
  
  