---
title: '명령줄 관리 도구: SqlLocalDB | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apilocation:
- sqluserinstance.dll
ms.assetid: dd0882b1-a8a9-447a-8bdf-0f9d7f36d336
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a41daed808b51df59ba80e0113b84e46c501c9b4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68126953"
---
# <a name="command-line-management-tool-sqllocaldbexe"></a>명령줄 관리 도구: SqlLocalDB.exe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SqlLocalDB.exe는 사용자가 명령줄에서 LocalDB 인스턴스를 쉽게 관리할 수 있는 간단한 도구입니다. 이 도구는 LocalDB 인스턴스 API에 대한 단순 래퍼로 구현되어 있습니다. SQLCMD 등의 비슷한 여러 SQL Server 도구와 마찬가지로 매개 변수는 SqlLocalDB에 명령줄 인수로 전달되며 출력은 콘솔로 보내집니다.  
  
 SqlLocalDB를 사용하면 개발자는 API를 호출하는 코드를 작성할 필요 없이 LocalDB를 사용하거나 다른 도구를 이용하여 자동으로 작업을 수행할 수 있습니다.  
  
## <a name="sqllocaldb-options"></a>SqlLocalDB 옵션  
 SqlLocalDB에서는 다음과 같은 옵션을 지원합니다.  
  
|옵션|수행하는 작업|  
|------------|------------------|  
|`-?`|도움말 텍스트를 인쇄합니다.|  
|`create\|c "instance name" [version-number] [-s]`|지정한 이름과 버전으로 새 LocalDB 인스턴스를 만듭니다.<br /><br /> [버전 번호] 매개 변수를 생략하면 기본값으로 SqlLocalDB 빌드 버전이 사용됩니다.<br /><br /> -s는 인스턴스가 만들어진 후 새 LocalDB 인스턴스를 시작합니다.|  
|`delete\|d "instance name"`|지정한 이름의 LocalDB 인스턴스를 삭제합니다.|  
|`start\|s "instance name"`|지정한 이름으로 LocalDB 인스턴스를 시작합니다.|  
|`stop\|p "instance name" [-i\|-k]`|현재 쿼리의 실행을 완료한 후 지정한 이름의 LocalDB 인스턴스를 중지합니다.<br /><br /> -i는 NOWAIT 옵션을 사용하여 LocalDB 인스턴스 종료를 요청합니다.<br /><br /> -k는 프로세스와 접촉하지 않고 LocalDB 인스턴스 프로세스를 중지합니다.|  
|`share\|h ["owner SID or account"] "private name" "shared name"`|지정한 공유 이름을 사용하여 지정한 프라이빗 인스턴스를 공유합니다. 사용자 SID 또는 계정 이름을 생략하면 기본값으로 현재 사용자가 사용됩니다.|  
|`unshare\|u "shared name"`|지정한 공유 LocalDB 인스턴스의 공유를 취소합니다.|  
|`info\|i`|현재 사용자가 소유하고 있는 모든 기존 LocalDB 인스턴스와 모든 공유 LocalDB 인스턴스를 나열합니다.|  
|`info\|i "instance name"`|지정한 LocalDB 인스턴스에 대한 정보를 인쇄합니다.|  
|`versions\|v`|컴퓨터에 설치된 모든 LocalDB 버전을 나열합니다.|  
|||  
|`trace\|t on\|off`|추적을 설정하고 해제합니다.|  
  
 SqlLocalDB에서는 공백을 구분 기호로 처리하므로 공백 및 공백 문자가 포함된 인스턴스 이름은 따옴표로 묶어야 합니다. 예를 들면 다음과 같습니다.  
  
 `SqlLocalDB create "My instance name with spaces"`  
  
  
