---
title: 변경 데이터 캡처를 사용 하도록 설정 하려는 경우 cdc 스키마를 제거 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092946"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>변경 데이터 캡처를 사용할 계획인 경우 cdc 스키마를 제거합니다.
  데이터베이스에는 cdc 스키마가 포함되어 있습니다. 업그레이드 후에 변경 데이터 캡처를 사용하려면 먼저 이 cdc 스키마를 삭제해야 합니다. 데이터베이스에서 변경 데이터 캡처를 사용하도록 설정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 cdc라는 이름으로 새 스키마를 만듭니다.  
  
  
