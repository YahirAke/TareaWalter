<script setup>
import dayjs from 'dayjs';
import { onMounted } from 'vue';
import { ref } from 'vue';

const info = ref('');
const alum = ref('');

let evaluados = 0;
let total = 0;
let periodo = '';


let porcentajes = 0;

async function fetchData() {
    try {
        const response = await fetch('https://sitmotul.com.mx/api/statusEval')
        const data = await response.json();
        info.value = data
        // isLoading.value = false
        evaluados = info.value['alEvaluados'];
        document.getElementById('evaluados').innerHTML = evaluados;
        document.getElementById('grafic_evaluados').style.width = porcentaje(info.value['alEvaluados'], info.value['alTotal']);
        document.getElementById('porc_evaluados').innerHTML = porcentaje(info.value['alEvaluados'], info.value['alTotal']);

        total = info.value['alTotal'];
        document.getElementById('total').innerHTML = total;
        //fecha_inicio = formatear_fecha();
        const fecha_i = dayjs();
        const fecha_f = dayjs(formatear_fecha(info.value['fin']));
        const fecha_inicio = fecha_f.diff(fecha_i, 'hour');
        document.getElementById('fecha_rest').innerHTML = fecha_inicio.toString();
        //var fecha_total = fecha_fin-fecha_inicio;
        periodo = info.value['periodo'];

        console.log(info.value);
    } catch (error) {
        console.error('Error al obtener datos:', error);
    }
}

function formatear_fecha(dato) {
    const fechaHoraISO = dato;
    const fechaHora = new Date(fechaHoraISO);

    // Obtener componentes de la fecha y hora
    const year = fechaHora.getFullYear();
    const month = fechaHora.getMonth() + 1; // Los meses en JavaScript van de 0 a 11
    const day = fechaHora.getDate();

    // Formatear la fecha
    const fechaFormateada = `${year}-${month < 10 ? '0' : ''}${month}-${day < 10 ? '0' : ''}${day}`;
    return fechaFormateada;
}

function porcentaje(valor, total_t) {
    let porcent = (100 / total_t) * valor;
    porcent = Math.round(porcent);
    return (porcent + '%');
}


async function fetchData1() {
    try {
        const response = await fetch('https://sitmotul.com.mx/api/statusEvalIng')
        const data = await response.json();
        alum.value = data
        // isLoading.value = false
        //ISC
        let valor_totalISc = alum.value['ISC']['listas'] + alum.value['ISC']['faltantes'];
        document.getElementById('por_ISCL').innerHTML = porcentaje_alumnos(alum.value['ISC']['listas'], valor_totalISc) + '%';
        document.getElementById('por_ISCF').innerHTML = porcentaje_alumnos(alum.value['ISC']['faltantes'], valor_totalISc) + '%';
        document.getElementById('cantISCT').innerHTML = valor_totalISc;
        document.getElementById('cantISCL').innerHTML = alum.value['ISC']['listas'];
        document.getElementById('cantISCF').innerHTML = alum.value['ISC']['faltantes'];
        document.getElementById('ISClistas').style.width = porcentaje(alum.value['ISC']['listas'], valor_totalISc);
        document.getElementById('ISCfaltantes').style.width = porcentaje(alum.value['ISC']['faltantes'], valor_totalISc);

        //IE
        let valor_totalIE = alum.value['IE']['listas'] + alum.value['IE']['faltantes'];
        document.getElementById('por_IEL').innerHTML = porcentaje_alumnos(alum.value['IE']['listas'], valor_totalIE) + '%';
        document.getElementById('por_IEF').innerHTML = porcentaje_alumnos(alum.value['IE']['faltantes'], valor_totalIE) + '%';
        document.getElementById('cantIET').innerHTML = valor_totalIE;
        document.getElementById('cantIEL').innerHTML = alum.value['IE']['listas'];
        document.getElementById('cantIEF').innerHTML = alum.value['IE']['faltantes'];
        document.getElementById('IElistas').style.width = porcentaje(alum.value['IE']['listas'], valor_totalIE);
        document.getElementById('IEfaltantes').style.width = porcentaje(alum.value['IE']['faltantes'], valor_totalIE);

        //IEM
        let valor_totalIEM = alum.value['IEM']['listas'] + alum.value['IEM']['faltantes'];
        document.getElementById('por_IEML').innerHTML = porcentaje_alumnos(alum.value['IEM']['listas'], valor_totalIEM) + '%';
        document.getElementById('por_IEMF').innerHTML = porcentaje_alumnos(alum.value['IEM']['faltantes'], valor_totalIEM) + '%';
        document.getElementById('cantIEMT').innerHTML = valor_totalIEM;
        document.getElementById('cantIEML').innerHTML = alum.value['IEM']['listas'];
        document.getElementById('cantIEMF').innerHTML = alum.value['IEM']['faltantes'];
        document.getElementById('IEMlistas').style.width = porcentaje(alum.value['IEM']['listas'], valor_totalIEM);
        document.getElementById('IEMfaltantes').style.width = porcentaje(alum.value['IEM']['faltantes'], valor_totalIEM);

        //IEM
        let valor_totalIER = alum.value['IER']['listas'] + alum.value['IER']['faltantes'];
        document.getElementById('por_IERL').innerHTML = porcentaje_alumnos(alum.value['IER']['listas'], valor_totalIER) + '%';
        document.getElementById('por_IERF').innerHTML = porcentaje_alumnos(alum.value['IER']['faltantes'], valor_totalIER) + '%';
        document.getElementById('cantIERT').innerHTML = valor_totalIER;
        document.getElementById('cantIERL').innerHTML = alum.value['IER']['listas'];
        document.getElementById('cantIERF').innerHTML = alum.value['IER']['faltantes'];
        document.getElementById('IERlistas').style.width = porcentaje(alum.value['IER']['listas'], valor_totalIER);
        document.getElementById('IERfaltantes').style.width = porcentaje(alum.value['IER']['faltantes'], valor_totalIER);

        //II
        let valor_totalII = alum.value['II']['listas'] + alum.value['II']['faltantes'];
        document.getElementById('por_IIL').innerHTML = porcentaje_alumnos(alum.value['II']['listas'], valor_totalII) + '%';
        document.getElementById('por_IIF').innerHTML = porcentaje_alumnos(alum.value['II']['faltantes'], valor_totalII) + '%';
        document.getElementById('cantIIT').innerHTML = valor_totalII;
        document.getElementById('cantIIL').innerHTML = alum.value['II']['listas'];
        document.getElementById('cantIIF').innerHTML = alum.value['II']['faltantes'];
        document.getElementById('IIlistas').style.width = porcentaje(alum.value['II']['listas'], valor_totalII);
        document.getElementById('IIfaltantes').style.width = porcentaje(alum.value['II']['faltantes'], valor_totalII);
        console.log(alum.value);
    } catch (error) {
        console.log('Error al obtener datos:', error);
    }
}

function porcentaje_alumnos(valor, total_t) {
    let porcent = (100 / total_t) * valor;
    porcent = Math.round(porcent);
    return porcent;
}
onMounted(() => {
    fetchData();
    fetchData1();
})

</script>

<template>
    <div class="flex flex-col w-[80%] items-center">
        <h1 class="text-center text-white text-3xl">Evaluaciones</h1>
        <div class="flex flex-col gap-y-2 px-[1%] lg:px-0 lg:w-[700px]">
            <div class="flex flex-col gap-y-2">
                <h1 class="text-center">Horas restantes: <span id="fecha_rest"></span> horas</h1>
                <h1 class="text-center">Periodo: {{ info['periodo'] }}</h1>
                <h1 class="text-center">Fecha Inicio: {{ formatear_fecha(info['inicio']) }}</h1>
                <h1 class="text-center text-bold">Fecha Fin: {{ formatear_fecha(info['fin']) }}</h1>
            </div>
            <div class="flex flex-col gap-y-2">
                <div class="flex flex-col gap-x-2">
                    <div class="flex items-center justify-center w-[100%] h-10 bg-red-600">
                        <label class="text-white">Total: <span id="total"></span></label>
                    </div>100% Total de alumnos
                </div>

                <div class="flex flex-col gap-x-2">
                    <div id="grafic_evaluados" class="flex items-center justify-center h-10 bg-red-600">
                        <label class="text-white">Evaluados: <span id="evaluados"></span></label>
                    </div>
                    <div><span id="porc_evaluados"></span> Alumnos evaluados</div>
                </div>
            </div>
        </div>
        <div class="flex flex-col gap-y-2 w-full">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-y-2">
                <div id="ISC" class="mt-6 w-full p-3">
                    <div class="flex flex-col gap-y-2 border-2 border-[#504f4f] bg-[#8a9597] rounded-lg p-3">
                        <div class="flex flex-col items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="70px" height="70px" viewBox="0 0 14 14">
                                <g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round">
                                    <circle cx="7" cy="2.5" r="1.5" />
                                    <circle cx="2" cy="11.5" r="1.5" />
                                    <circle cx="7" cy="11.5" r="1.5" />
                                    <circle cx="12" cy="11.5" r="1.5" />
                                    <path d="M2 10V8a1 1 0 0 1 1-1h8a1 1 0 0 1 1 1v2M7 4v6" />
                                </g>
                            </svg>
                            <h1 class="text-lg lg:text-2xl text-white">Sistemas Computacionales</h1>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div class="flex justify-center items-center w-full h-10 bg-blue-600">
                                <label class="text-white">Total: 100%</label>
                            </div>
                            <div class="text-sm lg:text-md"><span id="cantISCT" class="text-md lg:text-md"></span> Total
                            </div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="ISClistas" class="flex items-center justify-center h-10 bg-blue-500">
                                <label class="text-white">Listas: <span id="por_ISCL"></span></label>
                            </div>
                            <div class="text-sm lg:text-md"><span id="cantISCL" class="text-md lg:text-md"></span>
                                Completadas</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="ISCfaltantes" class="flex items-center justify-center h-10 bg-blue-400">
                                <label class="text-white">Faltantes: <span id="por_ISCF"></span></label>
                            </div>
                            <div class="text-sm lg:text-md"><span id="cantISCF" class="text-md lg:text-md"></span>
                                Pendientes</div>
                        </div>
                    </div>
                </div>

                <div id="IE" class="mt-6 w-full p-3">
                    <div class="flex flex-col gap-y-2 border-2 border-[#9e9e32] bg-[#d8d837] rounded-lg p-3">
                        <div class="flex flex-col items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="70px" height="70px" viewBox="0 0 14 14">
                                <g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round">
                                    <rect width="8" height="8" x="3" y="3" rx="1" />
                                    <path d="M5 3V.5M9 3V.5M3 9H.5M3 5H.5M9 11v2.5M5 11v2.5M11 5h2.5M11 9h2.5m-5-1.5h-2" />
                                </g>
                            </svg>
                            <h1 class="text-lg lg:text-2xl text-black">Electronica</h1>
                        </div>
                        <div class="flex flex-col gap-x-2">
                            <div id="IE-total" class="flex justify-center w-[100%] h-10 bg-blue-600">
                                <label class="text-white">Total: 100%</label>
                            </div>
                            <div class="text-sm lg:text-md"><span id="cantIET" class="text-md lg:text-md"></span>
                                Total</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IElistas" class="flex items-center justify-center h-10 bg-blue-500">
                                <label class="text-white">Listas: <span id="por_IEL"></span></label>
                            </div>
                            <div class="text-sm lg:text-md"><span id="cantIEL" class="text-md lg:text-md"></span>
                                Listas</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IEfaltantes" class="flex items-center justify-center h-10 bg-blue-400">
                                <label class="text-white">Faltantes: <span id="por_IEF"></span></label>
                            </div>
                            <div class="text-sm lg:text-md"><span id="cantIEF" class="text-md lg:text-md"></span> Pendientes
                            </div>
                        </div>
                    </div>
                </div>

                <div id="IEM" class="mt-6 w-full p-3">
                    <div class="flex flex-col gap-y-2 border-2 border-[#51a7a0] bg-[#5DC1B9] rounded-lg p-3">
                        <div class="flex flex-col items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="70px" height="70px" viewBox="0 0 36 36">
                                <path fill="currentColor"
                                    d="m32.57 15.72l-3.35-1a12.12 12.12 0 0 0-.47-1.32a7.49 7.49 0 0 1-6.14-6.16a11.82 11.82 0 0 0-1.33-.48l-1-3.31a.61.61 0 0 0-.59-.45h-3.38a.61.61 0 0 0-.58.43l-1 3.3a11.63 11.63 0 0 0-2.38 1l-3-1.62a.61.61 0 0 0-.72.11L6.2 8.59a.61.61 0 0 0-.11.72l1.62 3a11.63 11.63 0 0 0-1 2.37l-3.31 1a.61.61 0 0 0-.43.58v3.38a.61.61 0 0 0 .43.58l3.33 1a11.62 11.62 0 0 0 1 2.33l-1.64 3.14a.61.61 0 0 0 .11.72l2.39 2.39a.61.61 0 0 0 .72.11l3.09-1.65a11.65 11.65 0 0 0 2.3.94l1 3.37a.61.61 0 0 0 .58.43h3.38a.61.61 0 0 0 .58-.43l1-3.38a11.63 11.63 0 0 0 2.28-.94l3.11 1.66a.61.61 0 0 0 .72-.11l2.39-2.39a.61.61 0 0 0 .11-.72l-1.66-3.1a11.63 11.63 0 0 0 .95-2.29l3.37-1a.61.61 0 0 0 .43-.58v-3.41a.61.61 0 0 0-.37-.59ZM18 23.5a5.5 5.5 0 1 1 5.5-5.5a5.5 5.5 0 0 1-5.5 5.5Z"
                                    class="clr-i-solid--badged clr-i-solid-path-1--badged" />
                                <circle cx="30" cy="6" r="5" fill="currentColor"
                                    class="clr-i-solid--badged clr-i-solid-path-2--badged clr-i-badge" />
                                <path fill="none" d="M0 0h36v36H0z" />
                            </svg>
                            <h1 class="text-lg lg:text-2xl text-white">Electromecanica</h1>
                        </div>
                        <div class="flex flex-col gap-x-2">
                            <div id="IEM-total" class="flex items-center justify-center w-[100%] h-10 bg-green-600">
                                <label class="text-white">Total: 100%</label>
                            </div>
                            <div><span id="cantIEMT"></span> total alumnos</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IEMlistas" class="flex items-center justify-center h-10 bg-green-500">
                                <label class="text-white">Listas: <span id="por_IEML"></span></label>
                            </div>
                            <div><span id="cantIEML"></span> Listas</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IEMfaltantes" class="flex items-center justify-center h-10 bg-green-400">
                                <label class="text-white">Faltantes: <span id="por_IEMF"></span></label>
                            </div>
                            <div><span id="cantIEMF"></span> Alumnos evaluados</div>
                        </div>
                    </div>
                </div>

                <div id="IER" class="mt-6 w-full p-3">
                    <div class="flex flex-col gap-y-2 border-2 border-[#5a9e32] bg-[#5fb22f] rounded-lg p-3">
                        <div class="flex flex-col items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="70px" height="70px" viewBox="0 0 48 48">
                                <g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                    stroke-width="4">
                                    <path d="M31 43s-13 1-20-7S4 4 4 4s24-1 32 5s6 23 6 23" />
                                    <path d="M44 44s-11.18-8.449-18-16c-6.82-7.552-10-15-10-15m10 15l1-13m-1 13l-10-1" />
                                </g>
                            </svg>
                            <h1 class="text-lg lg:text-2xl text-white">Energias Renovables</h1>
                        </div>
                        <div class="flex flex-col gap-x-2">
                            <div id="IER-total" class="flex items-center justify-center w-[100%] h-10 bg-blue-600">
                                <label class="text-white">Total: 100%</label>
                            </div>
                            <div><span id="cantIERT"></span> total alumnos</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IERlistas" class="flex items-center justify-center h-10 bg-blue-500">
                                <label class="text-white">Listas: <span id="por_IERL"></span></label>
                            </div>
                            <div><span id="cantIERL"></span> Listas</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IERfaltantes" class="flex items-center justify-center h-10 bg-blue-400">
                                <label class="text-white">Faltantes: <span id="por_IERF"></span></label>
                            </div>
                            <div><span id="cantIERF"></span> Alumnos evaluados</div>
                        </div>
                    </div>
                </div>

                <div id="II" class="mt-6 w-full p-3">
                    <div class="flex flex-col gap-y-2 border-2 border-[#9d9d58] bg-[#F5F5DC] rounded-lg p-3">
                        <div class="flex flex-col items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="70px" height="70px" viewBox="0 0 24 24">
                                <g fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"
                                    stroke-width="2">
                                    <path
                                        d="M8.3 10a.7.7 0 0 1-.626-1.079L11.4 3a.7.7 0 0 1 1.198-.043L16.3 8.9a.7.7 0 0 1-.572 1.1Z" />
                                    <rect width="7" height="7" x="3" y="14" rx="1" />
                                    <circle cx="17.5" cy="17.5" r="3.5" />
                                </g>
                            </svg>
                            <h1 class="text-lg lg:text-2xl text-black">Industrial</h1>
                        </div>
                        <div class="flex flex-col gap-x-2">
                            <div id="II-total" class="flex items-center justify-center w-[100%] h-10 bg-blue-600">
                                <label class="text-white">Total: 100%</label>
                            </div>
                            <div><span id="cantIIT"></span> total alumnos</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IIlistas" class="flex items-center justify-center h-10 bg-blue-500">
                                <label class="text-white">Listas: <span id="por_IIL"></span></label>
                            </div>
                            <div><span id="cantIIL"></span>Listas</div>
                        </div>

                        <div class="flex flex-col gap-x-2">
                            <div id="IIfaltantes" class="flex items-center justify-center h-10 bg-blue-400">
                                <label class="text-white">Faltantes: <span id="por_IIF"></span></label>
                            </div>
                            <div><span id="cantIIF"></span>Alumnos evaluados</div>
                        </div>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>