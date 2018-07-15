---
title: 사용자 지정 사전을 사용하여 단어 분리기의 동작 사용자 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8e278d1-aeaa-48f1-a0c6-5de232c983e4
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2f4fb4134dd17efa37a169265e53af9910a8d153
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288559"
---
# <a name="customize-the-behavior-of-word-breakers-with-a-custom-dictionary"></a>사용자 지정 사전을 사용하여 단어 분리기의 동작 사용자 지정
  언어별 사용자 지정 사전 파일을 만들어 특정 언어에 대한 단어 분리기 동작을 사용자 지정할 수 있습니다. 예를 들어 단어 분리기에서 특정 용어 또는 패턴을 분리하지 못하도록 차단할 수 있습니다.  
  
 자세한 내용은 다음 SharePoint 문서를 참조하십시오.  
  
 [사용자 지정 사전 만들기(SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkId=215011)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 사용자 지정 사전 파일을 다음 폴더에 배치합니다.  
  
 `C:\Program Files\Microsoft SQL Server\<instance name>\MSSQL\Binn`  
  
 사용자 지정 사전 파일을 만들거나 변경한 후 다음 명령을 사용하여 SQL 전체 텍스트 데몬 시작 관리자를 다시 시작합니다.  
  
 `exec sp_fulltext_service 'restart_all_fdhosts'`  
  
  
