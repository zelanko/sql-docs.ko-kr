---
title: 클러스터 디스크 선택 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster disk selection
ms.assetid: 0d6b863d-5972-4a20-9990-64ee8016fea6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 156c17d7dae5c4de07033a96f2e936448d8d02ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66096502"
---
# <a name="cluster-disk-selection"></a>클러스터 디스크 선택
  
  **설치 마법사의** 클러스터 디스크 선택 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 페이지를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터를 위한 공유 클러스터 디스크 리소스를 선택할 수 있습니다. 클러스터 디스크에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터가 저장됩니다.  
  
 공유 클러스터 디스크는 클러스터 설치를 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 요구 사항이 아닙니다. SMB 파일 서버는 장애 조치 (failover) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 클러스터 설치에 지원 되는 저장소로, 설치를 완료 하기 전에 **데이터베이스 엔진-데이터 디렉터리** 페이지를 사용 하 여 지정할 수 있습니다.  
  
> [!WARNING]  
>  Analysis Services를 설치하도록 선택한 경우 공유 클러스터 디스크를 지정해야 합니다.  
>   
>  이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]장애 조치(failover) 클러스터 인스턴스에서 FILESTREAM을 사용하려면 공유 클러스터 디스크를 지정해야 합니다.  
  
## <a name="options"></a>옵션  
 **공유 디스크**  
 목록에서 단일 디스크를 선택합니다. 클러스터 디스크에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터가 저장됩니다.  
  
 하나의 디스크만 지정할 수 있습니다. 클러스터 쿼럼 리소스가 있는 그룹을 선택할 경우 경고가 표시됩니다. 클러스터 쿼럼 리소스에 설치하지 않는 것이 좋습니다.  
  
 **사용 가능한 공유 디스크**  
 사용 가능한 디스크 목록, 각 디스크가 공유 디스크로 정규화되었는지 여부 및 각 디스크 리소스에 대한 설명을 표시합니다.  
  
  
