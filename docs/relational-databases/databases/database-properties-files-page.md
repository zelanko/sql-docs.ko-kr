---
title: 데이터베이스 속성(파일 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ad314609fbd0515bef138f28358421b3656515d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="database-properties-files-page"></a>데이터베이스 속성(파일 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 새 데이터베이스를 만들 수 있으며 선택한 데이터베이스의 속성을 확인하거나 수정할 수 있습니다. 이 항목은 **새 데이터베이스(일반 페이지)** 와 기존 데이터베이스의 **데이터베이스 속성(파일 페이지)** 에 적용됩니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **데이터베이스 이름**  
 데이터베이스 이름을 추가하거나 표시합니다.  
  
 **소유자**  
 데이터베이스 소유자를 목록에서 선택하여 지정합니다.  
  
 **전체 텍스트 인덱싱 사용**  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 전체 텍스트 인덱싱이 항상 설정되어 있으므로 이 확인란은 선택된 채로 비활성화되어 있습니다. 자세한 내용은 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)을 참조하세요.  
  
 **데이터베이스 파일**  
 관련된 데이터베이스의 데이터베이스 파일을 추가, 보기, 수정 또는 제거합니다. 데이터베이스 파일의 속성은 다음과 같습니다.  
  
 **논리적 이름**  
 파일 이름을 입력하거나 수정합니다.  
  
 **파일 유형**  
 목록에서 파일 유형을 선택합니다. 파일 유형은 **데이터**, **로그**또는 **Filestream 데이터**가 될 수 있습니다. 기존 파일의 파일 유형은 수정할 수 없습니다.  
  
 메모리 최적화 파일 그룹에 파일(컨테이너)을 추가하려면 **Filestream 데이터** 를 선택합니다.  
  
 Filestream 데이터 파일 그룹에 파일 (컨테이너)을 추가하려면 FILESTREAM을 사용해야 합니다. [서버 속성(고급 페이지)](../../database-engine/configure-windows/server-properties-advanced-page.md) 대화 상자를 사용하여 FILESTREAM을 설정할 수 있습니다.  
  
 **파일 그룹**  
 목록에서 파일이 속한 파일 그룹을 선택합니다. 기본 파일 그룹은 PRIMARY입니다. **\<새 파일 그룹>** 을 선택하고 **새 파일 그룹** 대화 상자에 파일 그룹에 대한 정보를 입력하여 새 파일 그룹을 만들 수 있습니다. 새 파일 그룹은 **파일 그룹** 페이지에서도 만들 수 있습니다. 기존 파일의 파일 그룹은 수정할 수 없습니다.  
  
 메모리 최적화 파일 그룹에 파일(컨테이너)을 추가할 경우 **파일 그룹** 필드에 데이터베이스의 메모리 최적화 파일 그룹 이름이 채워집니다.  
  
 **처음 크기**  
 파일의 처음 크기를 MB 단위로 입력하거나 수정합니다. 이 값은 기본적으로 **모델** 데이터베이스의 값입니다.  
  
 FILESTREAM 파일의 경우 이 필드가 유효하지 않습니다.  
  
 메모리 최적화 파일 그룹의 파일에 대해서는 이 필드를 수정할 수 없습니다.  
  
 **자동 증가**  
 파일의 자동 증가 속성을 선택하거나 표시합니다. 이러한 속성은 최대 파일 크기에 도달했을 때 파일의 확장 방법을 제어합니다. 자동 증가 값을 편집하려면 원하는 파일의 자동 증가 속성 옆에 있는 편집 단추를 클릭하고 **자동 증가 변경** 대화 상자에서 값을 변경합니다. 이러한 값은 기본적으로 **모델** 데이터베이스의 값입니다.  
  
 FILESTREAM 파일의 경우 이 필드가 유효하지 않습니다.  
  
 메모리 최적화 파일 그룹의 파일에 대해서는 이 필드가 **제한 없음**이어야 합니다.  
  
 **경로**  
 선택한 파일의 경로를 표시합니다. 새 파일의 경로를 지정하려면 파일 경로 옆에 있는 편집 단추를 클릭하고 대상 폴더로 이동합니다. 기존 파일의 경로는 수정할 수 없습니다.  
  
 FILESTREAM 파일의 경우 경로는 폴더입니다. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 은 이 폴더에 기본 파일을 만듭니다.  
  
 **파일 이름**  
 파일 이름을 표시합니다.  
  
 이 필드는 메모리 최적화 파일 그룹의 파일을 포함한 FILESTREAM 파일에 유효하지 않습니다.  
  
 **추가**  
 데이터베이스에 새 파일을 추가합니다.  
  
 **제거**  
 선택한 파일을 데이터베이스에서 삭제합니다. 파일이 비어 있지 않으면 제거할 수 없습니다. 주 데이터 파일과 로그 파일은 제거할 수 없습니다.  
  
 파일에 대한 자세한 내용은 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
