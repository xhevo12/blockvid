<template>
  <q-page class="row justify-center items-center" padding>
    <div class="q-pt-lg full-width" style="max-width: 1000px">
      <div class="text-center">
        <div class="">
          <h1 class="text-h2 q-pt-none q-mt-none">
            block<span class="text-red-9">vid</span>
          </h1>
        </div>
        <div>
          <h2 class="text-overline">insieme per una corretta informazione</h2>
        </div>
      </div>
      <div class="text-center">
        <div class="row text-red-3">
          <div class="col">
            <span class="text-h6"
              ><b>{{
                totalInfectedItalyExploded.reduce((a, b) => {
                  return Number(a) + Number(b.total);
                }, 0)
              }}</b></span
            >
            ITALIA
            <br />
            <span class="text-body1"
              ><b>{{ totalHealeds }}</b></span
            >
            GUARITI |
            <span class="text-body1"
              ><b>{{ totalDeads }}</b></span
            >
            DECEDUTI
          </div>
          <div class="col">
            <span class="text-h6">
              <b>{{ totalInfected }}</b></span
            >
            MONDO
          </div>
        </div>
      </div>
    </div>

    <News />

    <div class="q-pt-lg full-width" style="max-width: 1000px">
      <div class="text-red-9 no-padding">
        <h2 class="text-h6"><q-icon name="map" /> Mappe interattive</h2>
      </div>
      <div class="q-pt-md">
        <iframe
          src="https://public.flourish.studio/visualisation/1437744/embed"
          frameborder="0"
          scrolling="no"
          height="800"
          class="full-width"
          title="Gedi Visual Map"
          style="margin; 0"
        ></iframe>
        <q-btn
          type="a"
          href="https://lab.gedidigital.it/gedi-visual/2020/coronavirus-i-contagi-in-italia/"
          target="_blank"
          label="Leggi altro"
          flat
          color="red-9"
        />
      </div>
      <div class="q-pt-md">
        <iframe
          src="https://dataviz.nbcnews.com/projects/20200122-coronavirus-world-count/index.html?initialWidth=760&amp;childId=embed-20200122-coronavirus-world-count&amp;parentTitle=Coronavirus%20map%3A%20The%20COVID-19%20virus%20is%20spreading%20across%20the%20world.%20Here%27s%20where%20cases%20have%20been%20confirmed.&amp;parentUrl=https%3A%2F%2Fwww.nbcnews.com%2Fhealth%2Fhealth-news%2Fcoronavirus-map-confirmed-cases-2020-n1120686"
          scrolling="no"
          marginheight="0"
          style="margin; 0"
          frameborder="0"
          title="A map of countries with confirmed coronavirus cases, updated daily."
          height="600"
          class="full-width"
        ></iframe>
        <q-btn
          type="a"
          href="https://www.nbcnews.com/health/health-news/coronavirus-map-confirmed-cases-2020-n1120686"
          target="_blank"
          label="Leggi altro"
          flat
          color="red-9"
        />
      </div>
      <div class="q-pt-md">
        <iframe
          src="https://public.flourish.studio/visualisation/1448957/embed"
          scrolling="no"
          marginheight="0"
          style="margin; 0"
          frameborder="0"
          title="A map of countries with confirmed coronavirus cases, updated daily."
          height="600"
          class="full-width"
        ></iframe>
        <q-btn
          type="a"
          href="https://public.flourish.studio/visualisation/1448957/?utm_source=embed&utm_campaign=visualisation/1448957"
          target="_blank"
          label="Leggi altro"
          flat
          color="red-9"
        />
      </div>
    </div>

    <div class="q-pt-lg full-width" style="max-width: 1000px">
      <div class="text-red-9 no-padding">
        <h2 class="text-h6"><q-icon name="done_all" /> Dati ufficiali</h2>
      </div>
      <q-table
        title="In italia"
        :data="totalInfectedItalyExploded"
        :columns="columnsItalyExploded"
        :filter="filterItalyExploded"
        :pagination.sync="paginationItalyExploded"
        class="no-padding"
        row-key="name"
      >
        <template v-slot:top-right>
          <q-input
            dense
            borderless
            debounce="300"
            v-model="filterItalyExploded"
            placeholder="Ricerca..."
          />
        </template>
        <template v-slot:bottom>
          Totale
          <div class="text-body1 q-ml-lg">
            <b>
              {{
                totalInfectedItalyExploded.reduce((a, b) => {
                  return Number(a) + Number(b.total);
                }, 0)
              }}
            </b>
            <q-btn
              type="a"
              href="http://www.protezionecivile.gov.it/attivita-rischi/rischio-sanitario/emergenze/coronavirus"
              target="_blank"
              label="Fonte: Protezione Civile"
              flat
              color="red-9"
            />
          </div>
        </template>
      </q-table>
    </div>

    <div class="q-pt-lg full-width" style="max-width: 1000px">
      <q-table
        title="Nel mondo"
        :data="covidData"
        :columns="columns"
        :filter="filter"
        row-key="name"
      >
        <template v-slot:top-right>
          <q-input
            dense
            borderless
            debounce="300"
            v-model="filter"
            placeholder="Ricerca..."
          >
          </q-input>
        </template>

        <template v-slot:bottom>
          <div class="text-caption">
            I dati sono aggiornati al {{ lastUpdate.format("DD-MM-YYYY") }}
            <q-btn
              type="a"
              href="https://github.com/CSSEGISandData/COVID-19"
              target="_blank"
              label="Leggi altro"
              flat
              color="red-9"
            />
          </div>
        </template>
      </q-table>
    </div>

    <div class="q-pt-lg full-width" style="max-width: 1000px">
      <div class="text-red-9 no-padding">
        <h2 class="text-h6">
          <q-icon name="healing" /> Proteggi te stesso e gli altri
        </h2>
      </div>
      <div class="row">
        <q-img
          src="https://www.who.int/images/default-source/health-topics/coronavirus/social-media-squares/blue-1.png"
          style="width: 50%"
        >
        </q-img>
        <q-img
          src="https://www.who.int/images/default-source/health-topics/coronavirus/social-media-squares/blue-2.png"
          style="width: 50%"
        >
        </q-img>
        <q-img
          src="https://www.who.int/images/default-source/health-topics/coronavirus/social-media-squares/blue-3.png"
          style="width: 50%"
        >
        </q-img>
        <q-img
          src="https://www.who.int/images/default-source/health-topics/coronavirus/social-media-squares/blue-4.png"
          style="width: 50%"
        >
        </q-img>
        <q-btn
          type="a"
          href="https://www.nbcnews.com/health/health-news/coronavirus-map-confirmed-cases-2020-n1120686"
          target="_blank"
          label="World Health Organization"
          flat
          color="red-9"
        />
      </div>
    </div>

    <div class="q-pt-lg full-width" style="max-width: 1000px">
      <q-card>
        <h4
          class="text-weight-bold text-center q-pt-sm"
          style="margin-top: 5px; margin-bottom: 15px"
        >
          Consigliato per te
        </h4>
        <div class="text-h5 q-pa-md">{{ questions[rand].q }}</div>
        <div class="text-body1 q-pa-md">
          {{ questions[rand].a }}
        </div>
        <div class="q-pt-md">
          <q-item class="right-align">
            <div>
              <q-btn
                type="a"
                href="http://www.salute.gov.it/nuovocoronavirus"
                target="_blank"
                label="Ministero della salute"
                flat
                color="red-9"
              />
            </div>
          </q-item>
        </div>
      </q-card>
    </div>
  </q-page>
</template>

<script>
import News from "./../components/News";

import moment from "./../boot/moment";
import { questions } from "../misc/questions";

export default {
  name: "PageIndex",
  components: {
    News
  },
  data() {
    return {
      endpoint:
        "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_daily_reports/",
      today: moment(),
      covidData: [],
      lastUpdate: moment(),
      questions: questions,
      rand: Math.floor(Math.random() * 10),
      columns: [
        {
          name: "country",
          label: "Paese/Stato",
          field: row => row[1],
          format: (val, row) => `${val}` + (row[0] ? ` [${row[0]}]` : ``),
          // sortable: true,
          align: "left",
          sort: 1
        },
        // {
        //   name: "province",
        //   required: true,
        //   label: "Provincia/Regione",
        //   align: "left",
        //   field: row => row[0],
        //   sortable: true
        // },
        {
          name: "confirmed",
          label: "Confermati",
          field: row => row[3],
          // sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        },
        {
          name: "deaths",
          label: "Morti",
          field: row => row[4],
          // sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        },
        {
          name: "recovered",
          label: "Guariti",
          field: row => row[5],
          // sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        },
        {
          name: "lastUpdate",
          label: "Ultimo aggiornamento",
          field: row => row[2]
          // sortable: true
        }
      ],
      filter: "",
      paginationItalyExploded: {
        rowsPerPage: 0,
        sortBy: "total",
        descending: true
      },
      filterItalyExploded: "",
      columnsItalyExploded: [
        {
          name: "region",
          label: "Regione",
          field: row => row.region,
          align: "left",
          sortable: true
        },
        {
          name: "total",
          label: "Totale",
          field: row => row.total,
          align: "left",
          sortable: true,
          sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)
        }
      ],
      showSource: false,
      totalInfectedItalyExploded: [
        {
          region: "Lombardia",
          total: 1820
        },
        {
          region: "Emilia Romagna",
          total: 544
        },
        {
          region: "Veneto",
          total: 360
        },
        {
          region: "Piemonte",
          total: 82
        },
        {
          region: "Campania",
          total: 31
        },
        {
          region: "Liguria",
          total: 26
        },
        {
          region: "Marche",
          total: 84
        },
        {
          region: "Toscana",
          total: 38
        },
        {
          region: "Lazio",
          total: 30
        },
        {
          region: "Friuli Venezia Giulia",
          total: 18
        },
        {
          region: "Puglia",
          total: 9
        },
        {
          region: "Sicilia",
          total: 18
        },
        {
          region: "Abruzzo",
          total: 7
        },
        {
          region: "Umbria",
          total: 9
        },
        {
          region: "Calabria",
          total: 1
        },
        {
          region: "Trentino Alto Adige",
          total: 6
        },
        {
          region: "Molise",
          total: 3
        },
        {
          region: "Basilicata",
          total: 1
        },
        {
          region: "Sardegna",
          total: 2
        }
      ],
      totalHealeds: 276,
      totalDeads: 107
    };
  },
  mounted() {
    this.prepareData(this.endpoint, this.today)
      .then(response => {
        this.covidData = response;
        this.formalize(response);
        this.lastUpdate = data;
      })
      .catch(error => {
        let endpoint = this.endpoint;
        let data = this.today.subtract(1, "days");

        this.prepareData(endpoint, data)
          .then(response => {
            this.covidData = response;

            this.formalize(response);
            this.lastUpdate = data;
          })
          .catch(error => {
            let endpoint = this.endpoint;
            let data = this.today.subtract(2, "days");

            this.prepareData(endpoint, data).then(response => {
              this.covidData = response;

              this.formalize(response);
              this.lastUpdate = data;
            });
          });
      });
  },
  methods: {
    prepareData(endpoint, date) {
      let finalEndpoint = endpoint + date.format("MM-DD-YYYY") + ".csv";
      return new Promise((resolve, reject) => {
        this.$axios
          .get(finalEndpoint)
          .then(response => {
            this.endpoint = finalEndpoint;
            let covidData = response.data.split("\n").map(row => {
              return row.split(",").length > 8
                ? row.split(",").unshift()
                : row.split(",");
            });
            covidData.shift();

            resolve(covidData);
          })
          .catch(error => {
            reject(error);
          });
      });
    },
    formalize(data) {
      let totalInfected = 0;
      let totalInfectedItaly = 0;

      data.forEach(row => {
        if (row.length == 9) {
          totalInfected += Number(row[4]);
        }
        if (row.length == 8) {
          totalInfected += Number(row[3]);
        }
        if (row[1] == "Italy") {
          if (row.length == 9) {
            totalInfectedItaly += Number(row[4]);
          }
          if (row.length == 8) {
            totalInfectedItaly += Number(row[3]);
          }
        }
      });

      this.$store.dispatch("setTotalInfected", totalInfected);
      this.$store.dispatch("setTotalInfectedItaly", totalInfectedItaly);
    }
  },
  computed: {
    leftDrawerOpen: {
      get() {
        return this.$store.state.leftDrawerOpen;
      },
      set() {
        this.$store.dispatch(
          "leftDrawerOpen",
          !this.$store.state.leftDrawerOpen
        );
      }
    },
    totalInfected() {
      return this.$store.state.totalInfected;
    },
    totalInfectedItaly() {
      return this.$store.state.totalInfectedItaly;
    }
  }
};
</script>
