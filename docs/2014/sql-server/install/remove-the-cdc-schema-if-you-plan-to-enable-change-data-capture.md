---
title: 변경 데이터 캡처를 사용 하도록 설정 하려는 경우 cdc 스키마를 제거 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cf7a9173e268b35f5a0a567a0812dc0e0b48ae91
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36181956"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>변경 데이터 캡처를 사용할 계획인 경우 cdc 스키마를 제거합니다.
  데이터베이스에는 cdc 스키마가 포함되어 있습니다. 업그레이드 후에 변경 데이터 캡처를 사용하려면 먼저 이 cdc 스키마를 삭제해야 합니다. 데이터베이스에서 변경 데이터 캡처를 사용하도록 설정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 cdc라는 이름으로 새 스키마를 만듭니다.  
  
  