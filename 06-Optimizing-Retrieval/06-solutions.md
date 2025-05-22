# Solutions for the Tasks from Journey 2

In this document you will find the solutions for the Tasks from Journey 2.

Let's have a look at the data of our search index and try to think how users might ask questions - and with which search query type the relevant chunks would be retrieved best!

1. Review content of the PerksPlus.pdf
2. Formulate two questions that users might ask about this content
3. Make assumptions about which search method will perform better (focus on keyword search vs. vector search)
4. Test the assumption by executing both searches and comparing the retrieved results.
___

## :question: Question Example 1

<details>
  <summary>:white_check_mark: See Example Question 1!</summary>

    "Can I expense the fees of my soccer club?"

    🔍 Assumption:
    - Keyword Search: May miss it unless "soccer" is explicitly mentioned (it's not).
    - Vector Search: Likely to succeed, since "sports team fees" is listed.

    Expected Outcome:
    ✅ Vector search performs better
    ❌ Keyword search misses or ranks irrelevant results

    
</details>

<details>
  <summary>:white_check_mark: See Code!</summary>

    question = "Can I expense the fees of my soccer club?"
    results_keyword = search_client.search(search_text=question, top=5, select=["title", "chunk"])

    print("Key word search results")
    display_results(results_keyword)

    results_vector = search_client.search(vector_queries=[VectorizableTextQuery(text=question, k_nearest_neighbors=50, fields="text_vector")], top=5, select=["title", "chunk"])

    print("Vector search results")
    display_results(results_vector)
    
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    Key word search results:

    | Title                                      | Chunk                                                                                                                                                                                                                       | @search.score |
    |--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
    | PerksPlus.pdf                              | PerksPlus Health and Wellness Reimbursement Program for Contoso Electronics Employees This document contains information generated using a language model (Azure OpenAI). The information contained in this document is only for demonstration purposes and does not reflect the ... | 5.810503      |
    | Northwind_Standard_Benefits_Details.pdf    | of calories to your diet, so try to avoid them. 6. Track your progress. Keeping track of your weight loss progress can help you to stay motivated and on track. 7. Seek support. Having a support system of friends, family, or a healthcare professional can help you to stay accountable and mo... | 4.774435      |
    | Northwind_Health_Plus_Benefits_Details.pdf | appointment safely by themselves. • The member is unable to travel to their appointment by public transportation. • The appointment is medically necessary and is covered by Northwind Health Plus. If you meet these criteria, you may be eligible to receive NEMT services. You will need to co... | 4.605549      |
    | Northwind_Standard_Benefits_Details.pdf    | from an in-network provider, it is important to understand that you may be responsible for a greater portion of the costs. Finally, it is important to be aware of any additional fees that may be associated with receiving care from an out-of-network provider. Some providers may charge additiona... | 4.408182      |
    | Northwind_Standard_Benefits_Details.pdf    | informed decisions about your healthcare. Be sure to read the plan document carefully to make sure that the plan meets your healthcare needs. WHAT IF I HAVE OTHER COVERAGE? Coordinating Benefits With Other Health Care Plans WHAT IF I HAVE OTHER COVERAGE? Coordinating Benefits With Other ... | 4.393216      |

    Vector search results:

    | Title                                      | Chunk                                                                                                                                                                                                                       | @search.score |
    |--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
    | PerksPlus.pdf                              | equipment purchases • Sports team fees • Health retreats and spas • Outdoor adventure activities (such as rock climbing, hiking, and kayaking) • Group fitness classes (such as dance, martial arts, and cycling) • Virtual fitness programs (such as online yoga and workout classes) In additi... | 0.809248      |
    | Northwind_Health_Plus_Benefits_Details.pdf | services. The plan pays for covered services after the member has met the annual deductible, up to the maximum out-of-pocket limit. The plan may also pay for services that are not listed in the plan documents, if the health care provider determines that such services are medically necessary. I... | 0.803715      |
    | Northwind_Standard_Benefits_Details.pdf    | service. Therefore, the insured may be responsible for paying any remaining balance, even if it is more than the Allowed Amount. Exceptions: In some cases, a service may not have an Allowed Amount or the Allowed Amount may be higher than the provider's charge. This may occur when the servic... | 0.801312      |
    | Northwind_Standard_Benefits_Details.pdf    | amount of the claim, and the amount that was paid by Northwind Health. Exceptions Northwind Standard does not cover emergency services, mental health and substance abuse services, or out-of-network services. Tips Before receiving any services, make sure to check with Northwind Health to... | 0.800327      |
    | Northwind_Standard_Benefits_Details.pdf    | to all services. For example, you may not be subject to the deductible when you receive in-network emergency services. Tips for Meeting the Calendar Year Deductible Meeting your calendar year deductible may seem like a daunting task, but there are a few steps you can take to help ensure tha... | 0.800301      |

</details>

___

## :question: Question Example 2

<details>
  <summary>:white_check_mark: See Example Question 2!</summary>

    "Is horseback riding considered eligible under PerksPlus?"

    🔍 Assumption:
    - Keyword Search: Strong — “horseback riding lessons” is explicitly listed.
    - Vector Search: Also strong, maybe even more flexible.

    Expected Outcome:
    🟡 Both work

    
</details>

<details>
  <summary>:white_check_mark: See Code!</summary>

    question = "Is horseback riding considered eligible under PerksPlus?"
    results_keyword = search_client.search(search_text=question, top=5, select=["title", "chunk"])

    print("Key word search results")
    display_results(results_keyword)

    results_vector = search_client.search(vector_queries=[VectorizableTextQuery(text=question, k_nearest_neighbors=50, fields="text_vector")], top=5, select=["title", "chunk"])

    print("Vector search results")
    display_results(results_vector)
    
</details>

<details>
  <summary>:white_check_mark: See Expected Answer!</summary>
  
    Key word search results:

    | Title                                      | Chunk                                                                                                                                                                                                                       | @search.score |
    |--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
    | PerksPlus.pdf                              | equipment purchases • Sports team fees • Health retreats and spas • Outdoor adventure activities (such as rock climbing, hiking, and kayaking) • Group fitness classes (such as dance, martial arts, and cycling) • Virtual fitness programs (such as online yoga and workout classes) In additi... | 12.768233     |
    | Northwind_Standard_Benefits_Details.pdf    | Northwind Standard plan offers a right of recovery for any services that were already paid for by the insured. This is a great feature for employees to be aware of, as it can help to save time and money. This right of recovery means that if the insured has already paid for a service that is co... | 7.433744      |
    | PerksPlus.pdf                              | PerksPlus Health and Wellness Reimbursement Program for Contoso Electronics Employees This document contains information generated using a language model (Azure OpenAI). The information contained in this document is only for demonstration purposes and does not reflect the ... | 6.615756      |
    | Northwind_Health_Plus_Benefits_Details.pdf | procedures that are typically done in a surgical center. All services must be medically necessary, and prior authorization may be required for some services. Exceptions There are some exceptions to coverage for surgical center care. The plan does not cover cosmetic or elective procedures, e... | 5.446031      |
    | Northwind_Health_Plus_Benefits_Details.pdf | questions or concerns about your coverage, it is important to contact Northwind Health Plus directly to ensure that you have the coverage you need. In addition to understanding the coverage you have, it is also important to understand the risks associated with surgery. It is important to discu... | 4.855504      |

  Vector Search Results:
  
    | Title                                      | Chunk                                                                                                                                                                                                                       | @search.score |
    |--------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
    | PerksPlus.pdf                              | equipment purchases • Sports team fees • Health retreats and spas • Outdoor adventure activities (such as rock climbing, hiking, and kayaking) • Group fitness classes (such as dance, martial arts, and cycling) • Virtual fitness programs (such as online yoga and workout classes) In additi... | 0.852140      |
    | PerksPlus.pdf                              | PerksPlus Health and Wellness Reimbursement Program for Contoso Electronics Employees This document contains information generated using a language model (Azure OpenAI). The information contained in this document is only for demonstration purposes and does not reflect the ... | 0.821478      |
    | Northwind_Health_Plus_Benefits_Details.pdf | ensure that your complaint or appeal is being addressed in a timely manner. OTHER INFORMATION ABOUT THIS PLAN Conformity With The Law OTHER INFORMATION ABOUT THIS PLAN – CONFORMITY WITH THE LAW Northwind Health Plus is in compliance with applicable state and federal laws and regulations,... | 0.813938      |
    | Northwind_Health_Plus_Benefits_Details.pdf | can help some people achieve major health benefits. Under this plan, coverage is available for certain types of weight loss surgeries, such as gastric bypass, gastric sleeve, and gastric banding. Exclusions and Limitations Please note that not all weight management services are covered unde... | 0.811016      |
    | Northwind_Health_Plus_Benefits_Details.pdf | • Talk to your doctor or health care provider about the trial and ask any questions you may have. • Ask about the potential risks and benefits of participating in the trial. • Ask about any potential side effects. • Ask if there are any costs associated with the trial that are not covered... | 0.807914      |


</details>
