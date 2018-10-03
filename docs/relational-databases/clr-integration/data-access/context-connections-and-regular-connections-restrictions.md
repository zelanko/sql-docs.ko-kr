---
title: 일반 및 컨텍스트 연결에 대 한 제한 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: 0c6fe4cb-d846-40b5-8884-35a9c770f5e8
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 800ec59fb837b167b1bcbffc61ddf7e8ce695849
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47641793"
---
# <a name="context-connections-and-regular-connections---restrictions"></a>컨텍스트 연결 및 일반 연결 - 제한 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스에서 컨텍스트 및 일반 연결을 통한 코드 실행과 관련된 제한 사항을 설명합니다.  
  
## <a name="restrictions-on-context-connections"></a>컨텍스트 연결에 대한 제한 사항  
 응용 프로그램을 개발할 때는 컨텍스트 연결에 적용되는 다음과 같은 제한 사항을 고려해야 합니다.  
  
-   지정된 시간에 지정된 연결에 대해 하나의 컨텍스트 연결만 열 수 있습니다. 별도의 연결에서 여러 문을 동시에 실행하는 경우 각 문에 대해 자체의 컨텍스트 연결이 생성됩니다. 이 제한 사항은 다른 연결의 동시 요청에는 적용되지 않으며 지정된 연결의 지정된 요청에만 적용됩니다.  
  
-   컨텍스트 연결에서는 MARS(Multiple Active Result Sets)가 지원되지 않습니다.  
  
-   **SqlBulkCopy** 클래스는 컨텍스트 연결에서 작동하지 않습니다.  
  
-   컨텍스트 연결에서는 업데이트 일괄 처리가 지원되지 않습니다.  
  
-   **SqlNotificationRequest** 는 컨텍스트 연결에 대해 실행되는 명령과 함께 사용할 수 없습니다.  
  
-   컨텍스트 연결에 대해 실행되고 있는 명령은 취소할 수 없습니다. **SqlCommand.Cancel** 메서드는 요청을 자동으로 무시합니다.  
  
-   "context connection=true"를 사용하는 경우 다른 연결 문자열 키워드를 사용할 수 없습니다.  
  
-   **SqlConnection.DataSource** 속성의 연결 문자열이 없으면 null을 반환 합니다 **SqlConnection** 는 "컨텍스트 연결 = true", 인스턴스의 이름 대신 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
-   명령이 컨텍스트 연결에 대해 실행되는 경우에는 **SqlCommand.CommandTimeout** 속성을 설정해도 아무 영향이 없습니다.  
  
## <a name="restrictions-on-regular-connections"></a>일반 연결에 대한 제한 사항  
 응용 프로그램을 개발할 때는 일반 연결에 적용되는 다음과 같은 제한 사항을 고려해야 합니다.  
  
-   내부 서버에 대한 비동기 명령 실행이 지원되지 않습니다. 명령의 연결 문자열에 "async=true"를 포함한 다음, 명령을 실행하면 **System.NotSupportedException** 이 throw됩니다. 그리고 " [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 프로세스 내에서 실행할 경우 비동기 처리가 지원되지 않습니다"라는 메시지가 표시됩니다.  
  
-   **SqlDependency** 개체가 지원되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [컨텍스트 연결](../../../relational-databases/clr-integration/data-access/context-connection.md)  
  
  
