---
title: 미국 영어 및 영국 영어에 사용되는 단어 분리기 변경 | Microsoft 문서
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
ms.assetid: 6b5d2177-db98-47f5-b32e-4b80a2f74ffe
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b0d8299581c5394b5528e9c42a41a64445fae800
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72903899"
---
# <a name="change-the-word-breaker-used-for-us-english-and-uk-english"></a>미국 영어 및 영국 영어에 사용되는 단어 분리기 변경
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서는 영어용 단어 분리기 및 형태소 분석기의 새 버전(버전 14.0.4999.1038)을 설치하여 이전 버전(버전 12.0.6828.0)의 해당 구성 요소를 대체합니다. 새 구성 요소의 변경된 동작에 대한 자세한 내용은 [전체 텍스트 검색의 동작 변경](/sql/database-engine/behavior-changes-to-full-text-search)을 참조하세요. 이 항목에서는 이러한 새 버전의 구성 요소에서 이전 버전으로 전환하거나 이전 버전에서 다시 새 버전으로 전환하는 방법에 대해 설명합니다. 클러스터 설치의 경우 이러한 변경은 모든 주 노드 및 패시브 노드에서 수행해야 합니다.  
  
 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 미국 영어(LCID 1033은)와 영국 영어(LCID 2057)에 대해 각기 다른 CLSID로 표시되는 서로 다른 단어 분리기가 사용되었습니다. 이번 릴리스에서는 다음 표와 같이 두 LCID 모두 동일한 CLSID를 갖는 동일한 구성 요소를 사용합니다.  
  
|LCID|이전 버전에서 설치된 단어 분리기<br /><br /> 버전 12.0.6828.0|이전 버전에서 설치된 형태소 분석기|이번 버전에서 설치되는 단어 분리기<br /><br /> 버전 14.0.4999.1038|이번 버전에서 설치되는 형태소 분석기|  
|----------|-------------------------------------------------------------------------|--------------------------------------------|-----------------------------------------------------------------------|---------------------------------------|  
|1033<br />(미국 영어)|188D6CC5-CB03-4C01-912E-47D21295D77E|EEED4C20-7F1B-11CE-BE57-00AA0051FE20|9faed859-0b30-4434-ae65-412e14a16fb8|e1e5ef84-c4a6-4e50-8188-99aef3de2659|  
|2057<br />(영국 영어)|173C97E2-AEBE-437C-9445-01B237ABF2F6|D99F7670-7F1A-11CE-BE57-00AA0051FE20|9faed859-0b30-4434-ae65-412e14a16fb8|e1e5ef84-c4a6-4e50-8188-99aef3de2659|  
  
 이 항목에서 설명하는 구성 요소는 `MSSQL\Binn` 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 폴더에 설치되는 DLL 파일입니다. 전체 경로는 일반적으로 `C:\Program Files\Microsoft SQL Server\<instance>\MSSQL\Binn`입니다.  
  
 단어 분리기 및 형태소 분석기에 대한 자세한 내용은 [검색을 위해 단어 분리기와 형태소 분석기 구성 및 관리](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)를 참조하세요.  
  
## <a name="switching-from-the-current-english-word-breaker-to-the-previous-english-word-breakers"></a>현재 영어 단어 분리기를 이전 영어 단어 분리기로 전환  
  
#### <a name="to-switch-from-the-current-version-of-the-us-english-word-breaker-to-the-previous-version"></a>현재 버전의 미국 영어 단어 분리기를 이전 버전으로 전환하려면  
  
1.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** 노드로 이동합니다.  
  
2.  다음 단계에 따라 LCID 1033의 이전 미국 영어 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  이전 단어 분리기의 **{188D6CC5-CB03-4C01-912E-47D21295D77E}** 값을 사용하여 새 키를 추가합니다.  
  
    2.  해당 키 값의 (기본값) 데이터를 **langwrbk.dll**로 업데이트합니다.  
  
    3.  이전 형태소 분석기의 **{EEED4C20-7F1B-11CE-BE57-00AA0051FE20}** 값을 사용하여 새 키를 추가합니다.  
  
    4.  해당 키 값의 (기본값) 데이터를 **infosoft.dll**로 업데이트합니다.  
  
3.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\enu** 노드로 이동합니다.  
  
4.  **WBreakerClass** 키 값을 **{188D6CC5-CB03-4C01-912E-47D21295D77E}** 로 업데이트합니다.  
  
5.  **StemmerClass** 키 값을 **{EEED4C20-7F1B-11CE-BE57-00AA0051FE20}** 으로 업데이트합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  

#### <a name="to-switch-from-the-current-version-of-the-uk-english-word-breaker-to-the-previous-version"></a>현재 버전의 영국 영어 단어 분리기에서 이전 버전으로 전환하려면  
  
1.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** 노드로 이동합니다.  
  
2.  다음 단계에 따라 LCID 2057의 이전 영국 영어 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  이전 단어 분리기의 **{173C97E2-AEBE-437C-9445-01B237ABF2F6}** 값을 사용하여 새 키를 추가합니다.  
  
    2.  해당 키 값의 (기본값) 데이터를 **langwrbk.dll**로 업데이트합니다.  
  
    3.  이전 형태소 분석기의 **{D99F7670-7F1A-11CE-BE57-00AA0051FE20}** 값을 사용하여 새 키를 추가합니다.  
  
    4.  해당 키 값의 (기본값) 데이터를 **infosoft.dll**로 업데이트합니다.  
  
3.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\eng** 노드로 이동합니다.  
  
4.  **WBreakerClass** 키 값을 **{173C97E2-AEBE-437C-9445-01B237ABF2F6}** 으로 업데이트합니다.  
  
5.  **StemmerClass** 키 값을 **{D99F7670-7F1A-11CE-BE57-00AA0051FE20}** 으로 업데이트합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
## <a name="switching-back-from-the-previous-english-word-breakers-to-the-current-english-word-breaker"></a>이전 영어 단어 분리기에서 다시 현재 영어 단어 분리기로 전환  
  
#### <a name="to-switch-back-from-the-previous-version-of-the-us-english-word-breaker-to-the-current-version"></a>이전 버전의 미국 영어 단어 분리기에서 현재 버전으로 전환하려면  
  
1.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** 노드로 이동합니다.  
  
2.  다음 키가 없으면 다음 단계에 따라 LCID 1033의 현재 미국 영어 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  현재 단어 분리기의 **{9faed859-0b30-4434-ae65-412e14a16fb8}** 값을 사용하여 새 키를 추가합니다.  
  
    2.  해당 키 값의 (기본값) 데이터를 **MsWb7.dll**로 업데이트합니다.  
  
    3.  현재 형태소 분석기의 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** 값을 사용하여 새 키를 추가합니다.  
  
    4.  해당 키 값의 (기본값) 데이터를 **MsWb7.dll**로 업데이트합니다.  
  
3.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\eng** 노드로 이동합니다.  
  
4.  **WBreakerClass** 키 값을 **{9faed859-0b30-4434-ae65-412e14a16fb8}** 로 업데이트합니다.  
  
5.  **StemmerClass** 키 값을 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** 로 업데이트합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
#### <a name="to-switch-back-from-the-previous-version-of-the-uk-english-word-breaker-to-the-current-version"></a>이전 버전의 영국 영어 단어 분리기에서 현재 버전으로 전환하려면  
  
1.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\CLSID** 노드로 이동합니다.  
  
2.  다음 키가 없으면 다음 단계에 따라 LCID 2057의 현재 영국 영어 단어 분리기 및 형태소 분석기 인터페이스에 대한 COM ClassID의 새 키를 추가합니다.  
  
    1.  현재 단어 분리기의 **{9faed859-0b30-4434-ae65-412e14a16fb8}** 값을 사용하여 새 키를 추가합니다.  
  
    2.  해당 키 값의 (기본값) 데이터를 **MsWb7.dll**로 업데이트합니다.  
  
    3.  현재 형태소 분석기의 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** 값을 사용하여 새 키를 추가합니다.  
  
    4.  해당 키 값의 (기본값) 데이터를 **MsWb7.dll**로 업데이트합니다.  
  
3.  레지스트리에서 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<InstanceRoot\>\MSSearch\Language\eng** 노드로 이동합니다.  
  
4.  **WBreakerClass** 키 값을 **{9faed859-0b30-4434-ae65-412e14a16fb8}** 로 업데이트합니다.  
  
5.  **StemmerClass** 키 값을 **{e1e5ef84-c4a6-4e50-8188-99aef3de2659}** 로 업데이트합니다.  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작합니다.  
  
## <a name="see-also"></a>참고 항목  
 [검색에 사용된 단어 분리기를 이전 버전으로 되돌리기](../../relational-databases/search/revert-the-word-breakers-used-by-search-to-the-previous-version.md)   
 [전체 텍스트 검색의 동작 변경](/sql/database-engine/behavior-changes-to-full-text-search)  
  
  
