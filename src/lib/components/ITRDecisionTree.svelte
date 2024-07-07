<script lang="ts">
  import { fly, slide } from "svelte/transition";
  import { quintOut } from "svelte/easing";

  type TaxFormData = {
    question: string;
    yes?: TaxFormData;
    no?: TaxFormData;
    result?: string;
  };

  let taxFormData: TaxFormData = {
    question: "Are you filing as an individual?",
    yes: {
      question: "Are you a resident of India for tax purposes?",
      yes: {
        question:
          "Do you have any income from Virtual Digital Assets (VDAs) like cryptocurrencies or NFTs?",
        yes: {
          result: "ITR-2",
        },
        no: {
          question:
            "Do you have income from lottery, gambling, or betting exceeding ₹10,000?",
          yes: {
            result: "ITR-2",
          },
          no: {
            question: "Is your agricultural income exceeding ₹5,000?",
            yes: {
              result: "ITR-2",
            },
            no: {
              question:
                "Is your total income for the financial year more than ₹50 lakhs?",
              yes: {
                question:
                  "Do you have foreign assets, foreign income, or income from foreign sources?",
                yes: {
                  result: "ITR-2",
                },
                no: {
                  question: "Do you have income from business or profession?",
                  yes: {
                    question:
                      "Is your business registered under MSMED Act and is your business turnover less than Rs. 2 crore?",
                    yes: {
                      question:
                        "Is your professional income less than Rs. 50 lakh?",
                      yes: {
                        result: "ITR-4 (Sugam)",
                      },
                      no: {
                        result: "ITR-3",
                      },
                    },
                    no: {
                      question:
                        "Do you have income under any presumptive business schemes (Section 44AD/44ADA/44AE)?",
                      yes: {
                        result: "ITR-4 (Sugam)",
                      },
                      no: {
                        result: "ITR-3",
                      },
                    },
                  },
                  no: {
                    question:
                      "Do you have income from capital gains exceeding the exemption limit, more than one house property, or income from other sources exceeding specified limits?",
                    yes: {
                      result: "ITR-2",
                    },
                    no: {
                      question:
                        "Do you have income only from salary, one house property, other sources (interest) up to specified limits, and agricultural income up to ₹5,000?",
                      yes: {
                        result: "ITR-1 (Sahaj)",
                      },
                      no: {
                        result: "ITR-2",
                      },
                    },
                  },
                },
              },
              no: {
                question: "Do you have income from business or profession?",
                yes: {
                  question:
                    "Is your business registered under MSMED Act and is your business turnover less than Rs. 2 crore?",
                  yes: {
                    question:
                      "Is your professional income less than Rs. 50 lakh?",
                    yes: {
                      result: "ITR-4 (Sugam)",
                    },
                    no: {
                      result: "ITR-3",
                    },
                  },
                  no: {
                    question:
                      "Do you have income under any presumptive business schemes (Section 44AD/44ADA/44AE)?",
                    yes: {
                      result: "ITR-4 (Sugam)",
                    },
                    no: {
                      result: "ITR-3",
                    },
                  },
                },
                no: {
                  question:
                    "Do you have income from capital gains exceeding the exemption limit, more than one house property, or income from other sources exceeding specified limits?",
                  yes: {
                    result: "ITR-2",
                  },
                  no: {
                    question:
                      "Do you have income only from salary, one house property, other sources (interest) up to specified limits, and agricultural income up to ₹5,000?",
                    yes: {
                      result: "ITR-1 (Sahaj)",
                    },
                    no: {
                      result: "ITR-2",
                    },
                  },
                },
              },
            },
          },
        },
      },
      no: {
        question:
          "Are you a Non-Resident Indian (NRI) or Not Ordinarily Resident (NOR)?",
        yes: {
          question:
            "Do you have any income from Virtual Digital Assets (VDAs) like cryptocurrencies or NFTs?",
          yes: {
            result: "ITR-2",
          },
          no: {
            question:
              "Do you have income only from salary, other sources (interest), and capital gains from specified securities?",
            yes: {
              result: "ITR-1 (Sahaj)",
            },
            no: {
              result: "ITR-2",
            },
          },
        },
        no: {
          question: "Do you qualify as a Deemed Resident?",
          yes: {
            result: "ITR-2",
          },
          no: {
            result: "Consult a tax expert for your specific situation",
          },
        },
      },
    },
    no: {
      question: "Are you filing as a Hindu Undivided Family (HUF)?",
      yes: {
        question:
          "Do you have any income from Virtual Digital Assets (VDAs) like cryptocurrencies or NFTs?",
        yes: {
          result: "ITR-2",
        },
        no: {
          question:
            "Is your income only from one house property, other sources (interest) up to specified limits, and agricultural income up to ₹5,000?",
          yes: {
            result: "ITR-1 (Sahaj)",
          },
          no: {
            question:
              "Do you have income under any presumptive business schemes (Section 44AD/44ADA/44AE)?",
            yes: {
              result: "ITR-4 (Sugam)",
            },
            no: {
              question: "Do you have income from business or profession?",
              yes: {
                result: "ITR-3",
              },
              no: {
                question:
                  "Do you have income from capital gains exceeding the exemption limit, or income from other sources exceeding specified limits?",
                yes: {
                  result: "ITR-2",
                },
                no: {
                  result: "ITR-1 (Sahaj)",
                },
              },
            },
          },
        },
      },
      no: {
        question: "Are you filing as a company?",
        yes: {
          question: "Is your company a recognized startup?",
          yes: {
            result: "ITR-6 (with special provisions)",
          },
          no: {
            question: "Is your company claiming exemption under section 11?",
            yes: {
              result: "ITR-7",
            },
            no: {
              result: "ITR-6",
            },
          },
        },
        no: {
          question: "Are you filing as a partnership firm?",
          yes: {
            result: "ITR-5",
          },
          no: {
            question: "Are you filing as a cooperative society?",
            yes: {
              result: "ITR-5",
            },
            no: {
              question: "Are you filing as a political party?",
              yes: {
                result: "ITR-7",
              },
              no: {
                question: "Are you filing as a charitable or religious trust?",
                yes: {
                  result: "ITR-7",
                },
                no: {
                  question:
                    "Are you filing as an association of persons (AOP) or body of individuals (BOI)?",
                  yes: {
                    result: "ITR-5",
                  },
                  no: {
                    question: "Are you filing as a local authority?",
                    yes: {
                      result: "ITR-7",
                    },
                    no: {
                      result:
                        "Consult a tax expert for your specific situation",
                    },
                  },
                },
              },
            },
          },
        },
      },
    },
  };

  let currentQuestion: TaxFormData = taxFormData;
  let history: { question: string; answer: "yes" | "no" }[] = [];
  let result: string | null = null;
  let loading: boolean = false;

  function handleAnswer(answer: "yes" | "no") {
    loading = true;
    setTimeout(() => {
      history = [...history, { question: currentQuestion.question, answer }];
      currentQuestion = currentQuestion[answer];
      if (currentQuestion?.result) {
        result = currentQuestion.result;
      }
      loading = false;
    }, 300);
  }

  function restart() {
    currentQuestion = taxFormData;
    history = [];
    result = null;
  }

  function goBack() {
    if (history.length > 0) {
      history = history.slice(0, -1);
      currentQuestion = taxFormData;
      for (let item of history) {
        currentQuestion = currentQuestion[item.answer];
      }
      result = null;
    }
  }
</script>

<div
  class="min-h-screen bg-gradient-to-br from-background to-background-light dark:from-background-dark dark:to-background text-text p-2 sm:p-4 md:p-8 flex flex-col items-center justify-center"
>
  <div
    class="w-full max-w-2xl bg-white dark:bg-background-light rounded-xl sm:rounded-2xl shadow-xl p-4 sm:p-6 md:p-8 border border-primary/10"
  >
    <h1
      class="text-2xl sm:text-3xl md:text-4xl font-extrabold mb-4 sm:mb-6 md:mb-8 text-center text-transparent bg-clip-text bg-gradient-to-r from-primary via-secondary to-accent"
    >
      Indian Tax Form Finder
    </h1>

    {#if result}
      <div
        in:fly={{ y: 20, duration: 500, easing: quintOut }}
        class="text-center"
      >
        <h2 class="text-lg sm:text-xl font-semibold mb-2 sm:mb-4">
          Your Recommended Tax Form:
        </h2>
        <p class="text-2xl sm:text-3xl font-bold text-secondary mb-4 sm:mb-6">
          {result}
        </p>
        <button
          on:click={restart}
          class="bg-gradient-to-r from-primary via-secondary to-accent text-white px-6 sm:px-8 py-2 sm:py-3 rounded-full hover:from-primary-dark hover:via-secondary-dark hover:to-accent-dark transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-primary focus:ring-opacity-50 shadow-lg text-sm sm:text-base"
        >
          Start Over
        </button>
      </div>
    {:else if currentQuestion?.question}
      <div
        in:fly={{ y: 20, duration: 500, easing: quintOut }}
        class="mb-4 sm:mb-6 md:mb-8"
      >
        <h2 class="text-lg sm:text-xl font-semibold mb-4 sm:mb-6 text-center">
          {currentQuestion.question}
        </h2>
        <div
          class="flex flex-col sm:flex-row justify-center space-y-2 sm:space-y-0 sm:space-x-4 md:space-x-6"
        >
          <button
            on:click={() => handleAnswer("yes")}
            class="bg-secondary text-white px-6 sm:px-8 py-2 sm:py-3 rounded-full hover:bg-secondary-dark transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-secondary focus:ring-opacity-50 shadow-lg text-sm sm:text-base"
            disabled={loading}
          >
            Yes
          </button>
          <button
            on:click={() => handleAnswer("no")}
            class="bg-accent text-white px-6 sm:px-8 py-2 sm:py-3 rounded-full hover:bg-accent-dark transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-accent focus:ring-opacity-50 shadow-lg text-sm sm:text-base"
            disabled={loading}
          >
            No
          </button>
        </div>
      </div>
    {:else}
      <p class="text-center text-base sm:text-lg">
        Something went wrong. Please try again.
      </p>
    {/if}

    {#if loading}
      <div class="flex justify-center items-center my-8">
        <div class="relative">
          <div
            class="w-10 h-10 rounded-full border-4 border-primary opacity-20 animate-ping"
          ></div>
          <div
            class="absolute top-0 left-0 w-10 h-10 rounded-full border-4 border-t-primary border-r-primary border-b-transparent border-l-transparent animate-spin"
          ></div>
        </div>
      </div>
    {/if}

    {#if history.length > 0}
      <div
        class="mt-6 sm:mt-8 md:mt-12 bg-background-light dark:bg-background p-4 sm:p-6 rounded-lg sm:rounded-xl shadow-inner"
      >
        <h3 class="text-base sm:text-lg font-semibold mb-3 sm:mb-4">
          Your Answers:
        </h3>
        <ul class="space-y-2 sm:space-y-3">
          {#each history as item, index (index)}
            <li
              in:slide={{ duration: 300 }}
              class="bg-white dark:bg-background-dark p-3 sm:p-4 rounded-lg shadow-sm flex flex-col sm:flex-row justify-between items-start sm:items-center space-y-1 sm:space-y-0"
            >
              <span class="font-medium text-xs sm:text-sm flex-grow mr-2"
                >{item.question}</span
              >
              <span
                class="text-text-muted text-xs sm:text-sm px-2 sm:px-3 py-1 bg-primary/10 rounded-full self-start sm:self-auto"
                >{item.answer}</span
              >
            </li>
          {/each}
        </ul>
        <button
          on:click={goBack}
          class="mt-4 sm:mt-6 text-primary hover:text-primary-dark transition-colors flex items-center group text-sm sm:text-base"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-4 w-4 sm:h-5 sm:w-5 mr-2 transform group-hover:-translate-x-1 transition-transform"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M9.707 14.707a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 1.414L7.414 9H15a1 1 0 110 2H7.414l2.293 2.293a1 1 0 010 1.414z"
              clip-rule="evenodd"
            />
          </svg>
          Go Back
        </button>
      </div>
    {/if}
  </div>
</div>
