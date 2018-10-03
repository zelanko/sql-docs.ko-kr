---
title: 개체 탐색기에서 인스턴스에 연결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7947bba9f41ffb77a1260ce79a5f4afb6c773295
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110933"
---
# <a name="connect-to-an-instance-from-object-explorer"></a>개체 탐색기에서 인스턴스에 연결
  개체 탐색기를 사용하여 개체를 관리하려면 먼저 개체가 포함된 인스턴스에 개체 탐색기를 연결해야 합니다. 동시에 여러 인스턴스에 개체 탐색기를 연결할 수 있습니다.  
  
## <a name="connecting-object-explorer-to-a-server"></a>개체 탐색기를 서버에 연결  
 개체 탐색기를 사용하려면 먼저 서버에 연결해야 합니다. 개체 탐색기 도구 모음에서 **연결** 을 클릭하고 드롭다운 목록에서 서버의 유형을 선택합니다. **서버에 연결** 대화 상자가 열립니다. 연결하려면 적어도 서버 이름과 올바른 인증 정보를 제공해야 합니다.  
  
## <a name="optional-object-explorer-connection-settings"></a>개체 탐색기 연결 설정(옵션)  
 서버에 연결할 때 **서버에 연결** 대화 상자에서 추가 연결 정보를 지정할 수 있습니다. **서버에 연결** 대화 상자는 마지막으로 사용된 설정을 보유하며 새 코드 편집기 창과 같은 새 연결에서 이러한 설정을 사용합니다.  
  
 연결 설정(옵션)을 지정하려면 다음 단계를 따르십시오.  
  
1.  개체 탐색기 도구 모음에서 **연결** 을 클릭하고 연결할 서버의 유형을 클릭합니다. **서버에 연결** 대화 상자가 표시됩니다.  
  
2.  **서버 이름** 상자에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 입력합니다.  
  
3.  **옵션**을 클릭합니다. **서버에 연결** 대화 상자에 추가 옵션이 표시됩니다.  
  
4.  **연결 속성** 탭을 클릭하여 추가 설정을 구성합니다. 사용할 수 있는 설정은 서버 유형에 따라 다릅니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 경우 다음 설정을 사용할 수 있습니다.  
  
    |설정|Description|  
    |-------------|-----------------|  
    |**데이터베이스에 연결**|서버에서 사용할 수 있는 데이터베이스 중에서 선택합니다. 사용자에게 볼 수 있는 권한이 있는 데이터베이스만 이 목록에 표시됩니다.|  
    |**네트워크 프로토콜**|공유 메모리, TCP/IP 또는 명명된 파이프 중에서 선택합니다.|  
    |**네트워크 패킷 크기**|바이트 단위로 구성합니다. 기본 설정은 4096바이트입니다.|  
    |**연결 제한 시간**|초 단위로 구성합니다. 기본 설정은 15초입니다.|  
    |**실행 제한 시간**|초 단위로 구성합니다. 기본 설정(0)은 실행의 제한 시간이 없음을 나타냅니다.|  
    |**연결 암호화**|강제로 암호화합니다.|  
  
5.  지정된 서버를 등록된 서버 목록에 추가하려면 **등록된 서버** 탭을 클릭하고 새 서버를 표시할 위치를 클릭한 다음 연결을 완료합니다.  
  
> [!NOTE]  
>  **추가 연결 매개 변수** 페이지를 사용하면 연결 문자열에 연결 매개 변수를 더 추가할 수 있습니다. 자세한 내용은 [서버에 연결&#40;추가 연결 매개 변수 페이지&#41;](../../database-engine/connect-to-server-additional-connection-parameters-page.md)을 참조하세요.  
  
  
