<template>
    <v-container fluid style="max-width: 1600px;">
        <div>
            <h1>Help - Command Line Interface</h1>
            <h2>pout2prot</h2>
            The Pout2Prot command line interface is a Python-package that can be easily installed using PiP. Pout2Prot
            requires at least Python 3.6 to work. All required dependencies will automatically be installed when using
            PiP, but you can also install the package from source by cloning our
            <a href="https://github.com/tivdnbos/pout2prot">GitHub repository</a>.
            <h3 class="mt-6">Installation</h3>
            <ul>
                <li>
                    First, make sure that a valid Python 3.6 installation is available on your system. If you're using
                    macOS you can use HomeBrew to install Python by running <span class="monospace">brew install
                    python3</span>. On Windows, you can find Python 3 in the Microsoft Store, which offers a one-click
                    installation process.
                </li>
                <li>
                    Execute <span class="monospace">pip --version</span>. If an error is shown or the output indicates
                    that this is a PiP-version that belongs to Python version 2, use <span class="monospace">pip3</span>
                    in the following commands.
                </li>
                <li>
                    Now, run <span class="monospace">pip install pout2prot</span> to install the application.
                </li>
            </ul>
            <h3 class="mt-6">Usage</h3>
            <div class="mb-4">
                The signature of the script is
                <div class="monospace code-block">
                    <span class="font-weight-black">
                        $ pout2prot [-h] [--occam] [--decoy_flag DECOY_FLAG] [--fdr_threshold FDR_THRESHOLD] input_folder groups_output_file subgroups_output_file
                    </span>
                </div>
            </div>

            <div class="mb-4">
                Three positional arguments are always required for the script to function properly:
                <ul>
                    <li>
                        <strong>input_folder:</strong> This argument should point to a folder that contains (i) one or
                        more *.pout files, or (ii) subfolders containing *.pout files in the case there are different
                        sample categories. In the latter case, the <span class="monospace">--sample_categories</span>
                        option should be used.
                    </li>
                    <li>
                        <strong>groups_output_file:</strong> Pointer to a location on the filesystem where the result file
                        with all protein groups should be stored.
                    </li>
                    <li>
                        <strong>subgroups_output_file:</strong> Pointer to a location on the filesystem where the result
                        file with all protein subgroups should be stored.
                    </li>
                </ul>
            </div>

            <div class="mb-4">
                Next to these mandatory arguments, the script can also be further modified by providing a value for
                these optional arguments:

                <ul>
                    <li>
                        <strong>occam:</strong> Should Occam's razor be enabled while determining protein groups? If
                        this option is not provided, Occam's razor will be disabled.
                    </li>
                    <li>
                        <strong>decoy_flag:</strong> If a value is provided for this parameter, all proteins that contain
                        this value as a substring will be considered as decoy proteins and will not be taken into account
                        during the analyses of the input files. This filter is disabled by default.
                    </li>
                    <li>
                        <strong>fdr_threshold:</strong> Filter out all proteins that have a FDR-threshold that's higher
                        than the value provided here. The default FDR-threshold that's used by this package is 0.01.
                    </li>
                </ul>
            </div>


            <h4>Example</h4>
            <div class="monospace code-block">
                <div class="font-weight-black">
                    $ pout2prot data/toy_examples/toy_example_1 groups_out.txt subgroups_out.txt
                </div>
            </div>
            <div class="my-2">
                Produces the following output files
            </div>
            <div class="monospace code-block">
                <div class="font-weight-black">
                    $ cat groups_out.txt
                </div>
                    sample category	sample name	protein accessions	spectrum count<br>
                    toy-examples	Examples_OccamsRazor_1	Prot3,Prot1,Prot2	3.0<br>
                    toy-examples	Examples_OccamsRazor_1	P2,P1,P3,P5,P4	6.0<br>
                    <br>
                <div class="font-weight-black">
                    $ cat subgroups_out.txt<br>
                </div>
                <div>
                    sample category	sample name	protein accessions	spectrum count<br>
                    toy-examples	Examples_OccamsRazor_1	Prot3	1.5<br>
                    toy-examples	Examples_OccamsRazor_1	Prot1,Prot2	1.5<br>
                    toy-examples	Examples_OccamsRazor_1	P2,P3,P1	2.3333333333333335<br>
                    toy-examples	Examples_OccamsRazor_1	P5	2.3333333333333335<br>
                    toy-examples	Examples_OccamsRazor_1	P4	1.3333333333333333<br>
                </div>
            </div>

            <h2 class="mt-12">pd2pout</h2>
            The <span class="monospace">pd2pout</span> command is a helper command provided by us that can be used to
            convert ProteomeDiscoverer files to pout-files, which can then be analysed by the
            <span class="monospace">pout2prot</span> command. This command is very easy to use.

            <h3 class="mt-6">Installation</h3>
            To install <span class="monospace">pd2pout</span> a valid Python 3.6 (or higher) installation is required,
            as well as pip. Installation of the package itself is then as simple as running
            <span class="monospace">pip install pd2pout</span>.

            <h3 class="mt-6">Usage</h3>
            <div class="mb-4">
                The signature of the script is
                <div class="monospace code-block mb-2">
                    <span class="font-weight-black">
                        $ pd2pout [-h] input_folder output_folder
                    </span>
                </div>

                All <span class="monospace">files</span> in the input_folder will be converted to
                <span class="monospace">pout</span> files that are stored in the output_folder.
            </div>
        </div>
    </v-container>
</template>

<script>
export default {
    name: "DocumentationPage"
}
</script>

<style scoped>
    .monospace {
        font-family: 'Roboto Mono', monospace;
        background-color: #ddd;
    }

    .code-block {
        border: 1px solid gray;
        padding: 4px;
    }
</style>
