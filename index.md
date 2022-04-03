---
title: Istruzioni online
permalink: index.html
layout: home
ms.openlocfilehash: c8816b7d9de9c19fbd4c6b3f373d6e4336c6ca5a
ms.sourcegitcommit: 26c283fffdd08057fdce65fa29de218fff21c7d0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/27/2022
ms.locfileid: "137908178"
---
# <a name="content-directory"></a>Directory contenuto

Collegamenti ipertestuali a ogni procedura dettagliata. Gli istruttori possono scegliere di usare la procedura dettagliata come dimostrazione o come lab per gli studenti. 

## <a name="walkthroughs"></a>Procedure dettagliate

{% assign wts = site.pages | where_exp:"page", "page.url contains '/Instructions/Walkthroughs'" %}
| Modulo | Procedura dettagliata |
| --- | --- | 
{% for activity in wts %}| {{ activity.wts.module }} | [{{ activity.wts.title }}{% if activity.wts.type %} - {{ activity.wts.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}

