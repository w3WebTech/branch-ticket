<template>
  <div class="bg-[#FAFBFF] h-screen roboto-thin">
    <div v-if="loading == true" class="w-full md:max-w-3xl">
      <loader />
    </div>
    <div v-else>
      <!-- tabs -->
      <div
        class="container md:w-[90%] md:mx-auto bg-[#eeeff4] md:bg-white pt-10"
      >
       <div class="overflow-x-auto">
    <div class="flex space-x-8 px-2">
      <!-- Tab 1: Create Ticket -->
      <div
        @click="getTabId(3)"
        :class="['px-4 py-3 text-sm cursor-pointer whitespace-nowrap', setTab == 3 ? 'border-b-2 border-blue-600 font-bold text-blue-600' : 'text-blue-600 hover:border-b-2 hover:border-blue-600 hover:font-bold']"
      >
        Create Ticket
      </div>

      <!-- Tab 2: Client Open Tickets -->
      <div
        @click="getTabId(1)"
        :class="[' py-3 text-sm cursor-pointer whitespace-nowrap', setTab == 1 ? 'border-b-2 border-blue-600 font-bold text-blue-600' : 'text-blue-600 hover:border-b-2 hover:border-blue-600 hover:font-bold']"
      >
        Client Open Tickets ({{ openTicketsCount && openTicketsCount.length }})
      </div>

      <!-- Tab 3: Client Resolved Tickets -->
      <div
        @click="getTabId(2)"
        :class="[' py-3 text-sm cursor-pointer whitespace-nowrap', setTab == 2 ? 'border-b-2 border-blue-600 font-bold text-blue-600' : 'text-blue-600 hover:border-b-2 hover:border-blue-600 hover:font-bold']"
      >
        Client Resolved Tickets ({{ resolvedTickets && resolvedTickets.length }})
      </div>

       <div
        @click="getTabId(4)"
        :class="['px-4 py-3 text-sm cursor-pointer whitespace-nowrap', setTab == 4 ? 'border-b-2 border-blue-600 font-bold text-blue-600' : 'text-blue-600 hover:border-b-2 hover:border-blue-600 hover:font-bold']"
      >
       branch open Tickets ({{ branchTicketData && branchTicketData.count }})
      </div>
          <div
        @click="getTabId(5)"
        :class="['px-4 py-3 text-sm cursor-pointer whitespace-nowrap', setTab == 5 ? 'border-b-2 border-blue-600 font-bold text-blue-600' : 'text-blue-600 hover:border-b-2 hover:border-blue-600 hover:font-bold']"
      >
       branch Resolved Tickets ({{ branchTicketDataResolved && branchTicketDataResolved.count }})
      </div>
    </div>
  </div>
        <!-- <div
          class="md:flex md:justify-between w-full md:items-center md:px-[10px]"
        >
          <div
            class="p-3 md:py-10 md:roboto-black md:roboto-bold-italic md:text-[30px]"
          >
            Hi {{ username && username }},<br />
            We are here to help you
          </div> -->
          <!-- <div class="md:block hidden pl-6">
            <button
              v-if="openTicketsCount"
              data-hs-overlay="#hs-vertically-centered-scrollable-modal"
              type="button"
              @click="openCreate"
              class="md:block hidden py-2 px-3 inline-flex justify-center items-center gap-x-2 text-sm font-semibold rounded-lg bg-blue-600 text-white hover:bg-[#2741b6] disabled:opacity-50 disabled:pointer-events-none"
            >
              Create Ticket
            </button>
          </div> -->
        <!-- </div> -->

        <!-- <div class="grid grid-cols-12 px-2">
          <div
            @click="getTabId(3)"
            :class="setTab == 3 ? 'border-b-2 border-blue-600 font-bold' : ''"
            class="col-span-4 hover:border-b-2 hover:border-blue-600 text-blue-600 hover:font-bold cursor-pointer"
          >
            <div class="text-center pb-3 text-sm">
            Create Ticket
            </div>
          </div>
          <div
            @click="getTabId(1)"
            :class="setTab == 1 ? 'border-b-2 border-blue-600 font-bold' : ''"
            class="col-span-4 hover:border-b-2 hover:border-blue-600 text-blue-600 hover:font-bold cursor-pointer"
          >
            <div class="text-center pb-3 text-sm">
             Client Open Tickets ({{ openTicketsCount && openTicketsCount.length }})
            </div>
          </div>
          <div
            @click="getTabId(2)"
            :class="setTab == 2 ? 'border-b-2 border-blue-600 font-bold' : ''"
            class="col-span-4 text-blue-600 hover:font-bold cursor-pointer"
          >
            <div class="text-center pb-3 text-sm">
             client Resolved tickets ({{ resolvedTickets && resolvedTickets.length }})
            </div>
          </div>
                  <div
            @click="getTabId(3)"
            :class="setTab == 3 ? 'border-b-2 border-blue-600 font-bold' : ''"
            class="col-span-4 text-blue-600 hover:font-bold cursor-pointer"
          >
            <div class="text-center pb-3 text-sm">
             client Resolved tickets ({{ resolvedTickets && resolvedTickets.length }})
            </div>
          </div>
        </div> -->
      </div>

      <!-- card -->
      <div
        class="pt-[15px] pb-14"
        :class="isCreate == true ? 'overflow-y-hidden' : ''"
      >
        <div
          v-if="setTab == 1"
          :class="isCreate == true ? 'overflow-y-hidden' : ''"
        >
          <openTicketsFlow :ticketData="this.openTicketsCount" />
        </div>
        <div
          v-if="setTab == 2"
          :class="isCreate == true ? 'overflow-y-hidden' : ''"
        >
          <resolvedTicketFlow :ticketData="this.resolvedTickets" />
        </div>
           <div
          v-if="setTab == 3"
          :class="isCreate == true ? 'overflow-y-hidden' : ''"
        >
          <createtickettab @go-to-home="goBackFunc" />
        </div>
            <div
          v-if="setTab == 4"
          :class="isCreate == true ? 'overflow-y-hidden' : ''"
        >
          <branchTickets :ticketData="this.branchTicketData" />
        </div>
         <div
          v-if="setTab == 5"
          :class="isCreate == true ? 'overflow-y-hidden' : ''"
        >
          <branchResolvedTicket :ticketData="this.branchTicketDataResolved" />
        </div>
      </div>
      <!-- <div class="fixed-bottom p-3 md:hidden block">
        <button
          v-if="openTicketsCount"
          data-hs-overlay="#hs-vertically-centered-scrollable-modal"
          type="button"
          @click="openCreate"
          class="w-full py-4 px-6 inline-flex justify-center items-center gap-x-2 text-sm font-semibold rounded-md bg-blue-600 text-white hover:bg-[#2741b6] disabled:opacity-50 disabled:pointer-events-none"
        >
          Create Ticket
        </button>
      </div> -->
      <!-- <createTicket /> -->
      <div v-if="isCreate">
        <createNewTicket @go-to-home="goBackFunc" />
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import axios from "axios";
export default {
  mounted() {
    this.fetchTickets();
    this.branchFetchTickets();
    this.branchResolvedFetchTickets();
  },
  data() {
    return {
      selectedTicket: null,
      openReview: false,
      loading: true,
      openTicketsCount: [],
      setTab: 1,
      isCreate: false,
      resolvedCount: [],
branchTicketData:[],
   branchTicketDataResolved:[],
      username: null,
      emailId: null,
    };
  },
  methods: {
    async fetchTickets(this: {
      emailId: any;
      resolvedTickets: any;
      openTicketsCount: any;
      loading: boolean;
      $emit: Function;
    }) {
      this.emailId = localStorage.getItem("clientemail");
      this.username = localStorage.getItem("clientname");
      const formData = new FormData();
      formData.append("emailId", this.emailId);

      try {
        const response = await axios.post(
          "https://g1.gwcindia.in/ticket-api/get-user-all-tickets.php",
          formData
        );

        this.openTicketsCount = response.data.data.filter(
          (item: any) =>
            item.status.name === "Open" || item.status.name === "In-Progress"
        );
        console.log(this.openTicketsCount, " this.openTicketsCount ");
        this.resolvedTickets = response.data.data.filter(
          (item: any) =>
            item.status.name === "Closed" ||
            item.status.name === "Awaiting Reply"
        );
        console.log(this.resolvedTickets, " this.resolvedTickets ");
      } catch (error) {
        error.message || "An error occurred";
      } finally {
        this.loading = false;
      }
    },
    
    refreshPage() {
      window.location.reload();
    },
    goBackFunc(ticket) {

      this.resolvedTickets = ticket
    .filter(
      (item) =>
        item.status.name === "Closed" || item.status.name === "Awaiting Reply"
    )
    .map((ticket) => ({ ...ticket }));
      console.log(this.resolvedTickets, " this.resolvedTickets ");
     this.openTicketsCount = ticket
    .filter(
      (item) =>
        item.status.name === "Open" || item.status.name === "In-Progress"
    )
    .map((ticket) => ({ ...ticket }));

  // Filter tickets for closed and awaiting reply statuses, and create shallow copies

      console.log("Tickets data received:", ticket);
      this.isCreate = false;
      document.body.style.overflow = "auto";
    },
    ticketsCount(this: { openTicketsCount: any }, count: any) {
      this.openTicketsCount = count;
    },
    resolvedTicketsCount(this: { resolvedCount: any }, count: any) {
      this.resolvedCount = count;
    },
    getTabId(this: { setTab: any }, id: any) {
      this.setTab = id;
      this.fetchTickets();
    },
    openCreate(this: { isCreate: boolean }) {
      this.isCreate = true;
      document.body.style.overflow = "hidden";
    },
      async branchFetchTickets() {
      
      try {
        const response = await axios.post(
          "https://g1.gwcindia.in/ticket-api/open-tickets.php?branchCode=CAD&createdBy=BRANCH"
        );


this.branchTicketData=response.data;
console.log(this.branchTicketData,"fff")
      } catch (error) {
        error.message || "An error occurred";
      } finally {
        this.loading = false;
      }
    },
     async branchResolvedFetchTickets() {
      
      try {
        const response = await axios.post(
          "https://g1.gwcindia.in/ticket-api/resolved-tickets.php?branchCode=CAD"
        );


this.branchTicketDataResolved=response.data;
console.log(this.branchTicketDataResolved,"checkbranchTicketDataResolved")
      } catch (error) {
        error.message || "An error occurred";
      } finally {
        this.loading = false;
      }
    },
  },
};
</script>
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
.fixed-bottom {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  /* z-index: 1000; */
  background-color: #ffffff;
}
.fixed-top {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  /* z-index: 1000; */
  /* background-color: #ffffff; */
}
.roboto-thin {
  font-family: "Roboto", sans-serif;
  font-weight: 500;
  color: black;
  font-style: normal;
}

.roboto-light {
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  font-style: normal;
}

.roboto-regular {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  font-style: normal;
}

.roboto-medium {
  font-family: "Roboto", sans-serif;
  font-weight: 500;
  font-style: normal;
}

.roboto-bold {
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  font-style: normal;
}

.roboto-black {
  font-family: "Roboto", sans-serif;
  font-weight: 900;
  font-style: normal;
}

.roboto-thin-italic {
  font-family: "Roboto", sans-serif;
  font-weight: 100;
  font-style: italic;
}

.roboto-light-italic {
  font-family: "Roboto", sans-serif;
  font-weight: 300;
  font-style: italic;
}

.roboto-regular-italic {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  font-style: italic;
}

.roboto-medium-italic {
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  font-style: italic;
}

.roboto-bold-italic {
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  font-style: italic;
}

.roboto-black-italic {
  font-family: "Roboto", sans-serif;
  font-weight: 900;
  font-style: italic;
}
</style>

