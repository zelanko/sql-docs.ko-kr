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
ms.openlocfilehash: abdb33fa3d1ff022a65ed569f19d48bcf4468501
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059149"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>변경 데이터 캡처를 사용할 계획인 경우 cdc 스키마를 제거합니다.
  데이터베이스에는 cdc 스키마가 포함되어 있습니다. 업그레이드 후에 변경 데이터 캡처를 사용하려면 먼저 이 cdc 스키마를 삭제해야 합니다. 데이터베이스에서 변경 데이터 캡처를 사용하도록 설정하면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 cdc라는 이름으로 새 스키마를 만듭니다.  
  
  
