<template>
    <select v-on:input="update($event.target.value)">
        <option v-for="region in regions" :key="region.value" :value="region.value">{{ includeValue(region.value) }}{{ region.label }}
        </option>
    </select>
</template>

<script>
    export default {
        name: "CloudRegionsSelect",

        props: {
            provider: {
                type: String,
                default: "aws",
                required: false
            },
            includeRegionCode: {
                type: Boolean,
                default: false,
                required: false
            },
            includeProviderPrefix: {
                type: Boolean,
                default: false,
                required: false
            },
            include: {
                type: Array,
                default: () => {
                    return [];
                },
                required: false
            },
            exclude: {
                type: Array,
                default: () => {
                    return [];
                },
                required: false
            }
        },
        data() {
            return {
                providers: {
                    aws: [
                        {value: "us-east-1", label: "US East (N. Virginia)"},
                        {value: "us-east-2", label: "US East (Ohio)"},
                        {value: "us-west-1", label: "US West (N. California)"},
                        {value: "us-west-2", label: "US West (Oregon)"},
                        {value: "ca-central-1", label: "Canada (Central)"},
                        {value: "eu-west-1", label: "EU (Ireland)"},
                        {value: "eu-central-1", label: "EU (Frankfurt)"},
                        {value: "eu-west-2", label: "EU (London)"},
                        {value: "eu-west-3", label: "EU (Paris)"},
                        {value: "eu-north-1", label: "EU (Stockholm)"},
                        {value: "ap-northeast-1", label: "Asia Pacific (Tokyo)"},
                        {value: "ap-northeast-2", label: "Asia Pacific (Seoul)"},
                        {value: "ap-southeast-1", label: "Asia Pacific (Singapore)"},
                        {value: "ap-southeast-2", label: "Asia Pacific (Sydney)"},
                        {value: "ap-south-1", label: "Asia Pacific (Mumbai)"},
                        {value: "sa-east-1", label: "South America (São Paulo)"},
                        {value: "us-gov-west-1", label: "US Gov West 1"},
                        {value: "us-gov-east-1", label: "US Gov East 1"}
                    ],
                    gcp: [
                        {
                            value: "asia-east1",
                            label: "Changhua County, Taiwan"
                        },
                        {
                            value: "asia-east2",
                            label: "Hong Kong"
                        },
                        {
                            value: "asia-northeast1",
                            label: "Tokyo, Japan"
                        },
                        {
                            value: "asia-northeast2",
                            label: "Osaka, Japan"
                        },
                        {
                            value: "asia-northeast3",
                            label: "Seoul, South Korea"
                        },
                        {
                            value: "asia-south1",
                            label: "Mumbai, India"
                        },
                        {
                            value: "asia-southeast1",
                            label: "Jurong West, Singapore"
                        },
                        {
                            value: "australia-southeast1",
                            label: "Sydney, Australia"
                        },
                        {
                            value: "europe-north1",
                            label: "Hamina, Finland"
                        },
                        {
                            value: "europe-west1",
                            label: "St. Ghislain, Belgium"
                        },
                        {
                            value: "europe-west2",
                            label: "London, England, UK"
                        },
                        {
                            value: "europe-west3",
                            label: "Frankfurt, Germany"
                        },
                        {
                            value: "europe-west4",
                            label: "Eemshaven, Netherlands"
                        },
                        {
                            value: "europe-west6",
                            label: "Zürich, Switzerland"
                        },
                        {
                            value: "northamerica-northeast1",
                            label: "Montréal, Québec, Canada"
                        },
                        {
                            value: "southamerica-east1",
                            label: "Osasco (São Paulo), Brazil"
                        },
                        {
                            value: "us-central1",
                            label: "Council Bluffs, Iowa, USA"
                        },
                        {
                            value: "us-east1",
                            label: "Moncks Corner, South Carolina, USA"
                        },
                        {
                            value: "us-east4",
                            label: "Ashburn, Northern Virginia, USA"
                        },
                        {
                            value: "us-west1",
                            label: "The Dalles, Oregon, USA"
                        },
                        {
                            value: "us-west2",
                            label: "Los Angeles, California, USA"
                        },
                        {
                            value: "us-west3",
                            label: "Salt Lake City, Utah, USA"
                        }
                    ],
                    do: [
                        {
                            value: "nyc1",
                            label: "New York City, United States (1)"
                        },
                        {
                            value: "nyc2",
                            label: "New York City, United States (2)"
                        },
                        {
                            value: "nyc3",
                            label: "New York City, United States (3)"
                        },
                        {
                            value: "ams2",
                            label: "Amsterdam, the Netherlands (1)"
                        },
                        {
                            value: "ams3",
                            label: "Amsterdam, the Netherlands (2)"
                        },
                        {
                            value: "sfo1",
                            label: "San Francisco, United States (1)"
                        },
                        {
                            value: "sfo2",
                            label: "San Francisco, United States (2)"
                        },
                        {
                            value: "sgp1",
                            label: "Singapore"
                        },
                        {
                            value: "lon1",
                            label: "London, United Kingdom"
                        },
                        {
                            value: "fra1",
                            label: "Frankfurt, Germany"
                        },
                        {
                            value: "tor1",
                            label: "Toronto, Canada"
                        },
                        {
                            value: "blr1",
                            label: "Bangalore, India"
                        }
                    ]
                },
                regions: []
            };
        },
        methods: {
            update(value) {
                this.$emit("input", this.includeProviderPrefix ? this.provider + '_' + value : value);
            },
            includeValue(value) {
                return this.includeRegionCode ? value + " - " : "";
            },
            filter() {
                let regions = this.providers[this.provider];

                if (this.include.length > 0) {
                    this.regions = regions.filter(item => {
                        return this.include.includes(item.value);
                    });
                }
                if (this.exclude.length > 0) {
                    this.regions = regions.filter(item => {
                        return !this.exclude.includes(item.value);
                    });
                }

                if (this.include.length === 0 && this.exclude.length === 0)
                    this.regions = regions;
            }
        },
        mounted() {
            this.filter();
        }
    };
</script>
