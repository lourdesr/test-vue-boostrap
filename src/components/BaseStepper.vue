<template>
    <div>
        <div class="container-fluid" style="padding-left: 0px; padding-right:0px;">
            <div class="row align-items-center justify-content-end mt--1 mb-4">
                <div class="col-12 col-lg-6 text-right">
                    <div class="btn-group">
                        <button class="btn btn-white dropdown-toggle" type="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                            Go to Step
                        </button>
                        <div class="dropdown-menu">
                            <a class="dropdown-item" style="cursor: pointer;" v-for="section in sections" :key="section.id" @click.prevent="goToStep(section.slug)">{{ section.id }} - {{ section.name }}</a>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row align-items-center mt-2 mb-4">
                <div class="col-2 col-lg-1 text-left" v-if="!section.prev"></div> <!--if no previous section, still create column to keep status bar aligned throughout all steps-->
                <div class="col-8 col-lg-10">
                    <h6 class="mb-4 text-uppercase text-center text-muted">
                            Step {{ section.id }} of {{ totalSections }}
                    </h6>
                    <div class="progress">
                        <div class="progress-bar" role="progressbar" :style="`width: ${stepPercentComplete}%;`" :aria-valuenow="25" :aria-valuemin="0" :aria-valuemax="100"></div>
                    </div>
                </div>
            </div>
            <component
                class="mt-4"
                :is="section['slug']"
                :name="section['name']"
                :section="section"
                :auction.sync="auction"
                :ref="section['slug']"
            >
            </component>

            <!-- NAV FOOTER -->
            <div class="row justify-content-center mt--4 mb-4">
                <div class="col-12 col-lg-10 col-xl-8">
                    <hr class="my-5">
                    <div class="nav row align-items-center">
                        <div class="col-auto" v-if="section.prev">
                            <button class="btn btn-white" @click.prevent="goToPrevSection(section)">Back</button>
                        </div>
                        <div class="col text-center">
                            <h6 class="text-uppercase text-muted mb-0">Step {{ section.id }} of {{ totalSections }}</h6>
                        </div>
                        <div class="col-auto" v-if="section.next">
                            <button class="btn btn-primary" @click.prevent="goToNextSection(section)">
                                <span v-if="section.slug === 'ffcp-forest-inventory'">
                                   Finish
                                </span>
                                <span v-else>
                                    Next
                                </span>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import PropertyDetails from '@/components/steps/PropertyDetails.vue';
import FeatureStep from '@/components/steps/FeatureStep.vue';
import CompareStep from '@/components/steps/CompareStep.vue';
import SpecificationStep from '@/components/steps/SpecificationStep.vue';
import SummaryStep from '@/components/steps/SummaryStep.vue';
export default {
  name: 'BaseStepper',
  components : {
    PropertyDetails,
    FeatureStep,
    CompareStep,
    SpecificationStep,
    SummaryStep
  },
  data () {
    return {
        currentStep: 1,
        auction : {
          data_txt_1: '',
          data_txt_2: '',
          data_txt_3: '',
          data_txt_4: '',
        },
        sections: [
            {
                id: 1,
                name: 'Property Details',
                slug: 'property-details',
                prev: null,
                next: 2
            },
            {
                id: 2,
                name: 'Comparison',
                slug: 'compare-step',
                prev: 1,
                next: 3
            },
            {
                id: 3,
                name: 'Features',
                slug: 'feature-step',
                prev: 2,
                next: 4
            },
            {
                id: 4,
                name: 'Specification',
                slug: 'specification-step',
                prev: 3,
                next: 5
            },
            {
                id: 5,
                name: 'Summary',
                slug: 'summary-step',
                prev: 4,
                next: null
            }
        ]
    };
  },
  computed: {
        section () {
            return this.sections.find(section => section.id === parseInt(this.currentStep));
        },

        totalSections () {
            return this.sections.length;
        },

        stepPercentComplete () {
            return Math.round((this.currentStep / this.totalSections) * 100);
        },
  },
  methods: {
        goToNextSection (section) {
            this.currentStep = section.next;
        },

        goToPrevSection (section) {
            this.currentStep = section.prev;
        },

        goToStep (stepslug) {
            const section = this.sections.find(section => section.slug === stepslug);
            this.currentStep = section.id;
        },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
