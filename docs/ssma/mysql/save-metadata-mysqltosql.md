---
description: 메타데이터 저장(MySQLToSQL)
title: 메타 데이터 저장 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9bc6273f-e8b1-430b-81a5-14330a783562
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b19ba78707fb596fde5ab73f04003a9d2d3feb9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418459"
---
# <a name="save-metadata--mysqltosql"></a>메타데이터 저장(MySQLToSQL)
**메타 데이터 저장** 대화 상자에 메타 데이터를 저장 하기 전에 ssma 프로젝트에 로드 하 라는 메시지가 표시 됩니다. 이를 통해 오프 라인으로 사용 하 고 기술 지원 담당자와 같은 다른 사람에 게 보낼 수 있는 전체 프로젝트 파일을 사용할 수 있습니다.  
  
**메타 데이터 저장** 대화 상자에 액세스 하려면 프로젝트를 저장 합니다. 메타 데이터가 없는 경우 SSMA는 **메타 데이터 저장** 대화 상자를 표시 합니다.  
  
## <a name="options"></a>옵션  
**이름**  
프로젝트에 있는 각 데이터베이스의 이름입니다.  
  
**상태**  
메타 데이터가 SSMA 프로젝트에 로드 되는지 또는 메타 데이터가 누락 되었는지 여부를 나타냅니다.  
  
SSMA는 필요에 따라 메타 데이터를 프로젝트에 로드 합니다. 메타 데이터는 메타 데이터를 찾아보고 스키마를 변환할 때 자동으로 로드 됩니다.  
  
**모두 선택**  
나열 된 모든 데이터베이스를 선택 합니다.  
  
**지우기**  
메타 데이터가 누락 된 모든 데이터베이스의 확인란을 선택 취소 합니다. 메타 데이터가 로드 된 경우에는이 확인란의 선택을 취소할 수 없습니다.  
  
**저장**  
메타 데이터가 누락 된 선택한 데이터베이스에 대 한 메타 데이터를 로드 하 여 프로젝트를 저장 합니다.  
  
**취소**  
저장 작업을 취소 합니다. 누락 된 메타 데이터가 프로젝트에 로드 되지 않았습니다.  
  
